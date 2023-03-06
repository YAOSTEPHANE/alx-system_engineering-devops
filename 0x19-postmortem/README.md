0x19. Postmortem

the issue occurred at 10:03 GMT in the consultaion of project 0x19. Post mortem
GET requests to the server led to 500 internal server errors, when the expected response was an HTML file defining a simple Holberton WordPress site. this problem affected all ALX students. the cause of this issue was -1 ENOENT (No such file or directory) occurring when trying to access the file /var/www/html/wp-includes/class-wp-locale.phpp.
Debug process
Bamidele debugger (Lexxyla…as in my actual initials…made it up on the spot, rather
well huh?) was tasked with solving the problem. I went through the files in the /var/www/html/ directory one by one, using Vim pattern matching to try to locate the wrong .phpp file extension. Locate it in the wp-settings.php file. (Line 137, require_once(ABSPATH.WPINC.’/class-wp-locale.php’);). Remove the trailing p from the line
Wrote a Puppet manifesto to automate the error fix.
Brief
a typo. I must love them. The entire WordPress application encountered a critical error in wp-settings.php when loading the class-wp-locale.phpp file. The correct filename located in the wp-content directory of the application folder, was class-wp-locale.php, the issue was resolved at 12:05 GMT.
Prevention
This failure was not a web server error, but an application error. To prevent such outages from continuing, please keep the following in mind.
Note that in response to this error I wrote a Puppet manifesto
0-strace_is_your_friend.pp
to automate the correction of these identical errors if they occur in the future.
