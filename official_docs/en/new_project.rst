Creating/founding a new database project
========================================

Any member of a database can create a new database project.

The new database project created will be completely independent from the current project and the founder will be its owner and sole user as long as he does not invite any new members to his project.

The steps to set up a project are as follows:

- You must give the project a unique name. This name will be the prefix name of your database tables and will be mostly seen in your browser URL.
- It is also necessary to give your project a short descriptive name that will appear in the header of our database project. This is already a translatable string, i.e. we can specify it in different languages later after the project is created.
- It is also necessary to write a detailed description of what the project is, what its purpose is. This can also be modified later.
- The possibilities to access and modify the data should be defined, which determines who can query and modify the data. In the case of closed projects, there are different levels of access to data after the project is created. This setting can be changed later.

When the project is created, a data table is created (with the name we have given it), containing only the fields required by OBM. This will be the base table of our project. We can define arbitrary data fields for this table during project creation, but we can also do this later in our project in a similar interface.

We need to specify the default center of the map page, which we can also modify later.

Finally, we need to specify the SRID of the base map of the project (https://spatialreference.org/), which defaults to WGS84 (epsg 4326).

After filling in and submitting this form, the project is created with an experimental status. This is not relevant for the functioning of the project, but rather for information of the users.

The user name and password valid for this project will also be used to access the newly created project.

After logging in to the project, a number of settings need to be made to make the project usable, such as setting up modules and creating forms.
