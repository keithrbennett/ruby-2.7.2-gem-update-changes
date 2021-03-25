This repo illustrates the changes made to a Ruby 2.7.2 system when `gem update --system` is applied to it.

You can see the changes by comparing the git commits. You can see a Github comparison at https://github.com/keithrbennett/ruby-2.7.2-gem-update-changes/compare/069173c..b16089f, but my favorite tool for this is RubyMine or other JetBrains IDE's; you can find the free and open source Intellij Idea community edition at https://www.jetbrains.com/idea/download/.

Here is the script that was used to create it:

```
#!/usr/bin/env ruby
 
set -x
 
\curl -sSL https://get.rvm.io | bash
cd .rvm
git init
echo .ri     > .gitignore
echo .idea/ >> .gitignore

git add .
git commit -m 'Installed rvm'

rvm install 2.7.2 --no-docs
rvm --default 2.7.2
git add .
git commit -m 'Installed 2.7.2'

gem -v > gem-version-before-gem-update
gem update --system -N
gem -v > gem-version-after-gem-update

git add .
git commit -m 'Ran gem update --system'

```

