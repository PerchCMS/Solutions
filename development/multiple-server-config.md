# How do I create a config file that will work on multiple servers?

## If you have a local, staging and live version of your Perch site then every time you move your files you have to be careful not to overwrite the config file. This solution explains how to create a file that switches on the hostname, meaning that it is safe to upload to all of your locations.

If you have a local, staging and live version of your Perch site then every time you move your files you have to be careful not to overwrite the config file. This solution explains how to create a file that switches on the hostname, meaning that it is safe to upload to all of your locations.

The default Perch config file looks like this:

    <?php
    define('PERCH_LICENSE_KEY', 'P21001-XXXXXX-XXXXXX-XXXXXX-XXXXXX');

    define("PERCH_DB_USERNAME", 'root');
    define("PERCH_DB_PASSWORD", 'xxxxxx');
    define("PERCH_DB_SERVER", "localhost");
    define("PERCH_DB_DATABASE", "db-site1");
    
    define('PERCH_EMAIL_FROM', 'me@mydomain.com');
    define('PERCH_EMAIL_FROM_NAME', 'Rachel Andrew');

    define('PERCH_LOGINPATH', '/perch');
    define('PERCH_PATH', str_replace(DIRECTORY_SEPARATOR.'config', '', dirname(__FILE__)));
    define('PERCH_CORE', PERCH_PATH.DIRECTORY_SEPARATOR.'core');


    define('PERCH_RESFILEPATH', PERCH_PATH . DIRECTORY_SEPARATOR . 'resources');
    define('PERCH_RESPATH', PERCH_LOGINPATH . '/resources');
    
    define('PERCH_HTML5', true);
  
    ?>

The bits we are concerned with are those which are different from one server to another, essentially these four lines:

    define("PERCH_DB_USERNAME", 'root');
    define("PERCH_DB_PASSWORD", 'xxxxxx');
    define("PERCH_DB_SERVER", "localhost");
    define("PERCH_DB_DATABASE", "db-site1");

Ideally things like your DB prefix, location of resources and the name of the Perch folder would be the same in all locations as you should try and replicate the live environment as much as possible.

We are going to use PHP to look at the hostname of the server we are currently on, and create a switch statement that will call a different set of credentials in depending on what that hostname is.

Just below your license key, using a plain text editor add the following line:

    $http_host = getenv('HTTP_HOST');

Now we create the switch statement using each of the values you have set up as domains for this license, this should replace the four lines defining this information:

    switch($http_host)
    {
    	case('mysite.local') :
    
    		define("PERCH_DB_USERNAME", 'root');
    		define("PERCH_DB_PASSWORD", 'xxxxxx');
    		define("PERCH_DB_SERVER", "localhost");
    		define("PERCH_DB_DATABASE", "db-site1");
    		break;
    
    	case('mysite.my-staging-server.com') :
    		define("PERCH_DB_USERNAME", 'staging_username');
    		define("PERCH_DB_PASSWORD", 'staging_password');
    		define("PERCH_DB_SERVER", "localhost");
    		define("PERCH_DB_DATABASE", "db-staging-database");
    		break;

	    default :
    		define("PERCH_DB_USERNAME", 'mysite_user');
    		define("PERCH_DB_PASSWORD", 'mysite_password');
    		define("PERCH_DB_SERVER", "localhost");
    		define("PERCH_DB_DATABASE", "db-mysite");
    		break;
        }

Essentially all the above is saying is that if the value in the parentheses after case matches the variable in $http_host, use this set of definitions. You just need to change the value in parentheses to match your sites.

I would suggest making the live domain default – that way it will be used whether you have www or not in front of the domain, or in the case of having multiple domains pointed to one site.

You can save the file and – assuming the details are correct – this will now work in each of the locations and you don’t need to worry about overwriting it.