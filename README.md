# putty cookbook

# Requirements
This cookbook requires the 'windows' cookbook

# Usage
This cookbook is for standalone installation or part of a role. 

# Attributes
The following attributes exist
[:putty][:url] - source
[:putty][:file] - file for not_if

# Recipes
putty::default

# install putty
windows_package "PuTTY version 0.63" do
  source node[:putty][:url]
  installer_type :inno
  action :install
  not_if {::File.exists?(node[:putty][:file])}
  not_if{reboot_pending?}
end



windows_reboot 60 do
  reason 'reboot needed'
  only_if {reboot_pending?}
end 

# Author

Author:: Todd Pigram (<todd@toddpigram.com>)
