# Airflow
Best practices and important tips in Airflow.
## Set the email alarm mechanism
If you want to set the mailbox alarm mechanism, you need to do these steps:

(1) Modify airflow.cfg

(2) Maintain the [email] as follow：

[email]

email_backend = airflow.utils.email.send_email_smtp

（3）Modify the [smtp] as follow:

[smtp]

smtp_host = 'your host IP address'

smtp_starttls = True

smtp_ssl = False

smtp_user = 'user name'

smtp_password = 'password'

smtp_port = 25

smtp_mail_from = 'airflow@example.com'

## Set the Web Authentication

If you want to set the Web Authentication, you need to do these steps:

(1) Modify airflow.cfg

(2) Modify the [webserver] as follow:

authenticate = True

auth_backend = airflow.contrib.auth.backends.password_auth

(3) input the command

When password auth is enabled, an initial user credential will need to be created before anyone can login. An initial user was not created in the migrations for this authentication backend to prevent default Airflow installations from attack. Creating a new user has to be done via a Python REPL on the same machine Airflow is installed.

First, navigate to the airflow installation directory: cd ~/airflow

Second, Execute python command as follows:

$ python3

Python 3.6.7 | packaged by conda-forge | (default, Nov 21 2018, 03:09:43)
[GCC 7.3.0] on linux

>import airflow

> from airflow import models, settings

> from airflow.contrib.auth.backends.password_auth import PasswordUser

> user = PasswordUser(models.User())

> user.username = 'new_user_name'

> user.email = 'new_user_email@example.com'

> user.password = 'set_the_password'

> session = settings.Session()

> session.add(user)

> session.commit()

> session.close()

> exit()



