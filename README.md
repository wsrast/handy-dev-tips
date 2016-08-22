# handy-dev-tips
I'm creating this repo as a dumping ground for all the useful
tips I've found and don't want to lose track of. These have all
saved me a lot of time and grief.

### Running WebStorm as your Git Diff/Merge Tool

WebStorm's diff tool is amazing, so using it for Git is a
no-brainer. Just add the following to your %userprofile%\.gitconfig
file.

	[merge]
		tool = webstorm
	[mergetool "webstorm"]
		cmd = cmd.exe //c "\"webstorm\" merge \"$LOCAL\" \"$REMOTE\" \"$BASE\" \"$MERGED\""
		trustExitCode = true
	[diff]
		tool = webstorm
	[difftool "webstorm"]
		cmd = cmd.exe //c "\"webstorm\" diff \"$LOCAL\" \"$REMOTE\""


### Setting Up NPM, Bower, Git and Python behind a corporate proxy
This is a real pain, and I can't say how many times I've had to
look this up on stackoverflow. So, here it is for posterity.

####Git
In your %userprofile%\.gitconfig file:

	[http]
		proxy = http://{{username}}:{{proxy pw}}@{{mycorpproxy}}.com:80
	[https]
		proxy = http://{{username}}:{{proxy pw}}@{{mycorpproxy}}.com:443
	[url "https://"]
		insteadOf = git://

Note that you'll have to replace anything in {{ }}. If you're not
sure what your proxy address is, take a look in internet explorer
under Settings >> Internet Options >> Connections tab >>
LAN Settings. It should be there, or it should be loading a .pac
file that you can download and view as a text file. Your proxy
URL will be in there somewhere.

####NPM
In your %userprofile%\.bowerrc file:

	{
		"proxy":"http://{{username}}:{{proxy pw}}@{{mycorpproxy}}.com:80",
		"https-proxy": "http://{{username}}:{{proxy pw}}@{{mycorpproxy}}.com:443",
		"registry": "http://bower.herokuapp.com",
		"directory":"./bower_components",
		"strict-ssl": false
	}

####Bower
In your %userprofile%\.npmrc file:

	proxy=http://{{username}}:{{proxy pw}}@{{mycorpproxy}}.com:80/
	https-proxy=http://{{username}}:{{proxy pw}}@{{mycorpproxy}}.com:443/

####Python
In your %userprofile%\AppData\Roaming\pip\pip.ini file, you'll need
to add the following. You will need to create this file and its 
parent folder if they don't already exist.

	[global]
    	trusted-host = pypi.python.org
    	proxy = http://{{username}}:{{proxy pw}}@{{mycorpproxy}}.com:80