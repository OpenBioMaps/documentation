Creating/founding a new database project
========================================

Any member of a database can create a new database project using the "Founding new project" form.

The new database project will be completely independent of the current project, and the founder will be its owner and sole user as long as he does not invite any new members.

The steps to set up a project are as follows:

- Give a unique name for the project. This name will be the prefix for your database tables and will be most visible in your browser URL. It is strongly recommended to use a single and short word as the project name!
- It is also necessary to give a short descriptive name that will appear in the header of our database project. This is already a translatable string, i.e. we can specify it in different languages later after the project is created. It is not recommended to be too long; rather, it should be only 2-3 words.
- It is necessary to write a detailed description of what the project is and what its purpose is. This can also be modified later.
- The possibilities to access and modify the data should be defined, which determines who can query and modify the data. For closed projects, there are different levels of access to data after the project is created. This setting can be changed later.
- You need to specify the default centre of the map page, which we can also modify later on the map-related admin interface.
- Finally, you have to specify the SRID of the base map of the project (https://spatialreference.org/), which defaults to WGS84 (EPSG 4326). It is not recommended to use something else.

Once the form has been completed and submitted, the project will be created in an experimental status. This is not relevant to the project's functioning, but rather for the users' information.

When the project is created, you will see a message about the creation process that includes the name and password of the project's SQL admin user. Save this. You will definitely need this.

You can access the newly created project with your existing username (email) and password. 

When the project is created, a data table (named as we have given it) is created, containing only the fields required by OBM. This will be the base table of our project. Once the project is created, you can add your fields to the base table or create additional tables in the administrative interface.

After logging in to the project, several settings need to be configured to make it usable, such as setting up modules and creating forms.

In a nutshell, the following settings should be done:

- Set up your data table(s).
- Set up upload forms.
- Set up an SQL query.
- Set up your map interface
- Set up modules for data query (e.g. text_filter, identify_points) and visualisation (results_asStable, results_buttons, results_summary).
