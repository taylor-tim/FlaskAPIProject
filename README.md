FlaskAPIProject
===============

Flask API Test Project
This is just a little API that takes an integer and responds with Fibonacci sequences up to the nth

Setup:

Well, there are a lot of options. If you want the easy way, pick RHEL-based or Ubu.

SSH into your server, get root access. Copy the following into a file, I like to call it setup.sh. Use your favorite editor and insert this:

RHEL-based:
<pre>
yum install -y python-pip git mod_wsgi
pip install virtualenv requests
cd /
git clone https://github.com/taylor-tim/FlaskAPIProject
cd /FlaskAPIProject
virtualenv flask
flask/bin/pip install flask
iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 5000 -j ACCEPT
service iptables save
service iptables restart
echo "#!/bin/sh" > /etc/init.d/startAPI
echo "/FlaskAPIProject/flask/bin/python /FlaskAPIProject/api.py" >> /etc/init.d/startAPI
chmod a+xr /etc/init.d/startAPI
ln -s /etc/init.d/startAPI /etc/rc5.d/S99zapi
ln -s /etc/init.d/startAPI /etc/rc3.d/S99zapi
/etc/init.d/startAPI &
</pre>

Ubuntu (if you run Deb, you should know how to edit this):
<pre>
apt-get update
apt-get install -y python-pip git uwsgi
pip install virtualenv requests
cd /
git clone https://github.com/taylor-tim/FlaskAPIProject
cd /FlaskAPIProject
virtualenv flask
flask/bin/pip install flask
ufw allow 5000
echo "#!/bin/sh" > /etc/init.d/startAPI
echo "/FlaskAPIProject/flask/bin/python /FlaskAPIProject/api.py" >> /etc/init.d/startAPI
chmod a+xr /etc/init.d/startAPI
ln -s /etc/init.d/startAPI /etc/rc5.d/S99zapi
ln -s /etc/init.d/startAPI /etc/rc3.d/S99zapi
/etc/init.d/startAPI &
</pre>
Then,
<pre>
chmod u+x setup.sh
<pre>
./setup.sh
</pre>
(or whatever you named it).

If you don't run RHEL-based or Ubu, you should know how to edit the above to make it work.

That's it. The API is up and running and will start on boot. 
