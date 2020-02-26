# apiprovider

<h3>API Provider command line file</h3>
<h4>Description</h4>
<p>
    This file helps you to create models easily without writing a single line of code, that helps also to build a well formed
    model that should not have problems during the api process.
</p>
<h4>Usage</h4>
<p>
    To use this file, enter to command line and switch to project directory then execute <code>php provider [OPTION [VALUE]]</code>
    Valid options are :
    <ul>
        <li><code>create_model Modelname</code> : This one creates a model with the given name</li>
        <li><code>create_preferred Modelname</code> : Create a preferred model under preferred directory</li>
        <li><code>clear</code> : This command deletes all models in project (critical usage)</li>
        <li><code>grant</code> : Used to give a model the permission to select, update, insert or delete</li>
        <li><code>revoke</code> : Used to delete model's permissions</li>
        <li><code>update</code> : update the API Provider to a higher version is exists (not available yet)</li>
    </ul>
    Example of use : php provider create_model Product<br />
    This will ask you fields of the model, the fields names <b>MUST</b> be the same in the database table, if you are done with fields
    then just let the next one empty and press <code>ENTER</code> to finish the process and you will get you model ready to be used.
</p>

<h3>API Provider CRUD</h3>
<h4>Description</h4>
<p>
    This API Provider comes with a built-in CRUD url that reduces you efforts to about 60%
</p>
<h4>Usage</h4>
<p>
    To use the API Provider API you will have first to configure the <code>.connection</code> file that contains 4 global variables to
    be able to connect to MySQL database.<br />
    File schema :<br />
    <ul>
        <li>hostname : usually localhost or alternatively 127.0.0.1</li>
    <li>username : MySQL database username (default is root)</li>
    <li>password : Your database password</li>
    <li>dbname : database name</li>
</ul>
<i>Ps : the file must not have white spaces ot empty lines</i>
<br />
To use CRUD links follow this link structure :<br />
<code>
    hostname/project_name/index.php?context=[CONTEXT]&action=[ACTION][&FIELD=VALUE[...]]
</code>
</p>

<h4>Valid CRUD actions</h4>
<p>
    The valid CRUD actions that are built with API Provider are : <br />
    <ul>
        <li><code>findAll</code> : give you the possibility to fetch all rows from a table</li>
        <li><code>find&column=?</code> : retrieve rows where a condition</li>
        <li><code>delete&column=?</code> : delete rows where a condition</li>
        <li><code>count</code> : counts total rows</li>
        <li><code>count&column=?</code> : counts rows where a condition</li>
    </ul>
</p>

<h4>Examples (project devcrawlers.com/api)</h4>
<p>
    Select all products : <code>https://devcrawlers.com/api/index.php?context=product&action=findAll</code><br/>
    Select a product with ID : <code>https://devcrawlers.com/api/index.php?context=product&action=find&id_pro=9</code><br/>
    Select all products cost 100$ : <code>https://devcrawlers.com/api/index.php?context=product&action=find&price=100</code><br/>
    Delete a product : <code>https://devcrawlers.com/api/index.php?context=product&action=delete&id_pro=2</code><br/>
    Count products : <code>https://devcrawlers.com/api/index.php?context=product&action=count</code><br/>
    Count products cost 100$ : <code>https://devcrawlers.com/api/index.php?context=product&action=count&price=100</code><br/>
</p>

<h3>Using Preferred Handler</h3>
<h4>Description</h4>
<p>
    The preferred handlers gives you the possibility to perform complex queries with a single line of code
</p>
<h4>Usage</h4>
<p>
    Use the provider command line to generate a custom handler then implement handle function using cases from given action<br />
</p>
<h4>Example</h4>
<p>
    Creating a query to retrieve all products and their categories, here is how the file must look like<br />
    <pre>
    &lt;?php

    class Mypreferredmodel extends PreferredHandler {

        public function handle(){
            // TODO add actions to take here (Handle both GET and POST methods)
            // Create Dracula instance and execute the query method
             switch ($this->getAction()){

                 case 'everything':
                     (new Logger())->json((new Dracula())->query("SELECT * FROM product NATURAL JOIN category", null));
                     break;

            }
        }

    }
    </pre>
    by accessing the 'everything' action you will get the json response.<br />
    <code>https://devcrawlers.com/api/index.php?context=mypreferredmodel&action=everything</code>

</p>

<br />
<hr>
2020 &copy; Crawlers Open Source, All Rights Reserved to <a href="https://devcrawlers.com" target="_blank">DevCrawlers</a>