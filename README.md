subversion Cookbook
===================
[![Build Status](https://secure.travis-ci.org/opscode-cookbooks/subversion.png?branch=master)](http://travis-ci.org/opscode-cookbooks/subversion)

Installs subversion for clients or sets up a server under Apache HTTPD.


Requirements
------------
Requires Chef version 0.10.10+ and Ohai 0.6.12, due to use of `platform_family`.

### Platforms
- Debian/Ubuntu
- RHEL/CentOS
- Fedora
- Windows


Cookbooks
---------
- apache2
- windows


Attributes
----------
See `attributes/default.rb` for default values. The attributes are used in the server recipe.

* `node['subversion']['version']` - version to install
* `node['subversion']['repo_dir']` - filesystem location of the repository to serve.
* `node['subversion']['repo_name']` - name of the repository to serve up.
* `node['subversion']['server_name']` - server name used in the svn vhost.
* `node['subversion']['user']` - user to log into the svn vhost.
* `node['subversion']['password']` - htpasswd for the subversion user in the server recipe. This should be overridden as the default is not secure.
* `node['subversion']['list_parent_path']` - a choice of "on" or "off".  When set to "on" the list of repositories in the `node['subversion']['repo_dir']` will be indexed at http://<server_name>/svn.  Default is "off"


Recipes
-------
### default
Includes `recipe[subversion::client]`.

### client
Installs `subversion` packages.

### server
Sets up an SVN repository server with `recipe[apache2::mod_dav_svn]`. This will use the `web_app` definition from the apache cookbook to drop off the template, and uses the attributes for configuration.


Usage
-----
On nodes where `subversion` should be installed such as application servers that will check out a repository, use `recipe[subversion]`. If you would like a subversion server, use `recipe[subversion::server]`. You should override `node['subversion']['password']` in the role that applies the server recipe.


License & Authors
-----------------
- Author:: Adam Jacob <adam@opscode.com>
- Author:: Joshua Timberman <joshua@opscode.com>
- Author:: Daniel DeLeo <dan@kallistec.com>

```text
Copyright:: 2008-2011, Opscode, Inc

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
````
