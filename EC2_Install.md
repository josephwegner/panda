About
=====

The following instructions were created for installing panda on an EC2 instance, running Ubuntu 12.04.1.  It should work on most future/past version of Ubuntu, but is in no way guaranteed.

Preinstallation
---------------

1. Update aptitude
  `sudo aptitude update`
2. Install `rubygems`, `subversion`, and `git-core`
  `sudo aptitude install rubygems subversion git-core`
3. Setup `rake`
  `sudo gem install rake`
4. You need a couple different versions of `sexp_processor`
     sudo gem install sexp_processor` --version 3.2.0
     sudo gem install sexp_processor` --version 4.0
     sudo gem install sexp_processor` --version 4.1
5. Install other rubygem dependencies
  `sudo gem install merb merb_helpers activesupport RubyInline amazon_sdb aws-s3 uuid flvtool2`
6. Install rVideo 0.9.4 **(0.9.3 is the current version.  Make sure you install 0.9.4)**
     svn checkout svn://rubyforge.org/var/svn/rvideo/trunk rvideo
     cd rvideo
     sudo ruby setup.rb
     cd ..
     sudo rm -r rvideo
7. Install the other system dependencies
  `sudo aptitude install libgd2 ffmpeg`

Panda Installation
------------------

1. Download Panda
  `git clone git://github.com/newbamboo/panda.git`
2. By default you are on the development branch.  If you'd like to use the stable version:
     cd panda
     git checkout -b stable origin/stable
     cd ..
3. Move panda to /var/www
  `sudo mv panda /var/www/`

Setup Nginx Webserver
---------------------
Nginx is the default supported webserver by Panda, so we're going to use that.
1.  Install Nginx.  We need the extras package, not just the default
  `sudo aptitude install nginx-extras`
2. Edit the config file `/var/www/panda/panda_nginx.conf.example`
  - Change `server_name` to your domain
  - If you would like the base URL to redirect somewhere, set `proxy_pass` and uncomment `proxy_redirect`
3. Remove the .example from the config file name
  `mv /var/www/panda/panda_nginx.conf.example /var/www/panda/panda_nginx.conf`
