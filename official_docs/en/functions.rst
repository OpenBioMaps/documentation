
´´´
BEGIN

IF tg_op = 'INSERT' THEN

    EXECUTE format('INSERT INTO %I_qgrids (row_id,original) SELECT %L,%L::geometry',TG_TABLE_NAME,NEW.obm_id,NEW.obm_geometry);

    EXECUTE format('UPDATE %I_qgrids SET "kef_5" = foo.geom FROM ( 
        SELECT obm_geometry AS geom
        FROM shared."kef_5x5"
        WHERE st_within(%L::geometry,obm_geometry)
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "kef_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom
        FROM shared."kef_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_2.5" = st_transform(foo.geom,4326) FROM ( 
        SELECT geometry as geom
        FROM shared."utm_2.5x2.5"
        WHERE st_within(%L::geometry,st_transform(geometry,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_100" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_100x100"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

RETURN NEW;
END IF;

IF tg_op = 'UPDATE' THEN

    EXECUTE format('UPDATE %I_qgrids SET "original"=%L::geometry WHERE row_id=%L', TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "kef_5" = foo.geom FROM ( 
        SELECT obm_geometry AS geom
        FROM shared."kef_5x5"
        WHERE st_within(%L::geometry,obm_geometry)
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "kef_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom
        FROM shared."kef_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_2.5" = st_transform(foo.geom,4326) FROM ( 
        SELECT geometry as geom
        FROM shared."utm_2.5x2.5"
        WHERE st_within(%L::geometry,st_transform(geometry,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_10" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_10x10"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

    EXECUTE format('UPDATE %I_qgrids SET "utm_100" = st_transform(foo.geom,4326) FROM ( 
        SELECT geom 
        FROM shared."utm_100x100"
        WHERE st_within(%L::geometry,st_transform(geom,4326))
    ) as foo WHERE row_id=%L',TG_TABLE_NAME,NEW.obm_geometry,NEW.obm_id);

RETURN NEW;
END IF;

IF tg_op = 'DELETE' THEN
    EXECUTE format('DELETE FROM %I_qgrids WHERE row_id=%L',TG_TABLE_NAME,OLD.obm_id);
RETURN OLD;
END IF;

END;
´´´
