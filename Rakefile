#
# Rakefile for Chef Solo "DNA" Repository
#
# Author:: Fletcher Nichol (<fnichol@nichol.ca>)
# Copyright:: Copyright (c) 2010 Fletcher Nichol
# License:: Apache License, Version 2.0
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

require 'rubygems'

TOPDIR = File.expand_path(File.dirname(__FILE__))

if File.directory?(File.join(TOPDIR, ".git"))
  $vcs = :git
end

desc "Update your repository from source control"
task :update do
  puts "** Updating your repository"

  case $vcs
  when :git
    pull = false
    IO.foreach(File.join(TOPDIR, ".git", "config")) do |line|
      pull = true if line =~ /\[remote "origin"\]/
    end
    if pull
      sh %{git pull} 
    else
      puts "* Skipping git pull, no origin specified"
    end
  else
    puts "* No git SCM configured, skipping update"
  end
end

