This is a silly commit.
## Katamari:

Katamari (塊, lit. "Mass", "Cluster", "Clump", or "Clod") is a harness
for the [Packaging](http://github.com/puppetlabs/packaging/) Repo.

## Why?

The Packaging Repo has accrued a number of tasks over the years, many
of which have nothing to do with packaging our products. A common work
flow seems to be "clone hiera, run `rake package:bootstrap`,
and then blahblahblahblah."

![Unacceptable!](http://permalink-bucket-ba0636a8-281c-4187-b20f-7d602600320b.s3.amazonaws.com/unacceptable-E6153B28-1D47-4069-A322-CB53FF662393.png "Unacceptable!")

But now you can use Katamari to safely work with the weird, not-quite-packaging tasks that have glommed onto the Packaging Repo without worrying about accidentally shipping an errant Hiera release.

## How?

```
mckern@flexo Repositories $ git clone git@github.com:mckern/katamari.git
mckern@flexo Repositories $ cd katamari
mckern@flexo katamari (git:master) $ rake -T
rake commits            # verify that commit messages match CONTRIBUTING.md requirements
rake package:bootstrap  # Bootstrap packaging automation, e.g
rake package:implode    # Remove all cloned packaging automation
rake rubocop            # run static analysis with rubocop
mckern@flexo katamari (git:master) $ rake package:bootstrap
cd ext
Cloning into 'packaging'...
remote: Counting objects: 6469, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6469 (delta 0), reused 0 (delta 0), pack-reused 6465
Receiving objects: 100% (6469/6469), 1.69 MiB | 1.31 MiB/s, done.
Resolving deltas: 100% (3510/3510), done.
Checking connectivity... done.
cd -
mckern@flexo katamari (git:master) $ rake -T
rake clean                                            # Clean all built packages, eg rm -rf pkg
rake commits                                          # verify that commit messages match CONTRIBUTING.md requirements
rake package:apple                                    # Task for building an Apple Package
rake package:bootstrap                                # Bootstrap packaging automation, e.g
rake package:deb                                      # Create a deb from this repo, using debuild (all builddeps must be installed)
rake package:implode                                  # Remove all cloned packaging automation
rake package:rpm                                      # Create .rpm from this git repository (unsigned)
rake package:srpm                                     # Create srpm from this git repository (unsigned)
rake package:tar                                      # Create a source tar archive
rake package:update                                   # Update your clone of the packaging repo with `git pull`
rake package:versionset                               # Set and commit the version in , requires VERSION
rake pe:jenkins:uber_build[poll_interval]             # Dynamic Jenkins UBER build: Build all the things with ONE job
rake pl:agent_tickets                                 # Create tickets to provide the agent stack for a new platform
rake pl:build_from_params                             # Build from a build params file
rake pl:check_rpm_sigs                                # Check if all rpms are signed
rake pl:deb                                           # Create a deb from this repo using the default cow 
rake pl:deb_all                                       # Create debs from this git repository using all cows specified in build_defa...
rake pl:fetch                                         # retrieve build-data configurations to override/extend local build_defaults
rake pl:jenkins:deb                                   # Queue pl:deb build on jenkins builder
rake pl:jenkins:deb_all                               # Queue pl:deb_all on jenkins builder
rake pl:jenkins:deb_repo_configs                      # Retrieve debian apt repository configs for this sha
rake pl:jenkins:deb_repos                             # Create apt repositories of build DEB packages for this SHA on the distribut...
rake pl:jenkins:generate_deb_repo_configs             # Create apt repository configs for package repos for this sha/tag on the dis...
rake pl:jenkins:generate_rpm_repo_configs             # Create yum repository configs for package repos for this sha/tag on the dis...
rake pl:jenkins:mock                                  # Queue pl:mock build on jenkins builder
rake pl:jenkins:mock_all                              # Queue pl:mock_all on jenkins builder
rake pl:jenkins:post[uri]                             # Trigger a jenkins uri with SHA of HEAD as a string param, requires "URI"
rake pl:jenkins:retrieve[remote_target,local_target]  # Retrieve packages from the distribution server
rake pl:jenkins:rpm_repo_configs                      # Retrieve rpm yum repository configs from distribution server
rake pl:jenkins:rpm_repos                             # Create yum repositories of built RPM packages for this SHA on the distribut...
rake pl:jenkins:ship[target,local_dir]                # Ship pkg directory contents to distribution server
rake pl:jenkins:ship_repo_configs                     # Ship generated repository configs to the distribution server
rake pl:jenkins:sign_all                              # Sign all locally staged packages on
rake pl:jenkins:tar                                   # Queue pl:tar build on jenkins builder
rake pl:jenkins:uber_build[poll_interval]             # Dynamic Jenkins UBER build: Build all the things with ONE job
rake pl:jenkins:uber_ship                             # Retrieve packages built by jenkins, sign, and ship all!
rake pl:mock                                          # Use default mock to make a final rpm, keyed to PL infrastructure, pass MOCK...
rake pl:mock_all                                      # Use specified mocks to make rpms, keyed to PL infrastructure, pass MOCK to ...
rake pl:print_build_param[param]                      # Print a build parameter
rake pl:print_build_params                            # Print all package build parameters
rake pl:puppet_agent_release_tickets                  # Make release tickets in JIRA for puppet-agent
rake pl:remote:deploy_apt_repo                        # Move signed deb repos from  to
rake pl:remote:deploy_yum_repos                       # Copy rpm repos from  to
rake pl:remote:update_apt_repo                        # Update remote apt repository on ''
rake pl:remote:update_ips_repo                        # Update remote ips repository on
rake pl:remote:update_yum_repo                        # Update remote yum repository on ''
rake pl:ship_debs                                     # Ship cow-built debs to
rake pl:ship_nuget                                    # ship Windows nuget packages to
rake pl:ship_p5p                                      # Ship p5p packages to
rake pl:ship_rpms                                     # Ship mocked rpms to
rake pl:ship_svr4                                     # Ship svr4 packages to
rake pl:ship_swix                                     # ship Arista EOS swix packages and signatures to
rake pl:ship_tar                                      # ship tarball and signature to
rake pl:sign_deb_changes                              # Sign generated debian changes files
rake pl:sign_ips                                      # Sign ips package, uses PL certificates by default, update privatekey_pem, c...
rake pl:sign_osx                                      # Sign OSX packages
rake pl:sign_rpms[root_dir]                           # Sign mocked rpms, Defaults to PL Key, pass GPG_KEY to override
rake pl:sign_svr4                                     # Detach sign any solaris svr4 packages
rake pl:sign_swix                                     # Sign the Arista EOS swix packages, defaults to PL key, pass GPG_KEY to over...
rake pl:sign_tar                                      # Sign the tarball, defaults to PL key, pass GPG_KEY to override or edit buil...
rake pl:tag                                           # Tag this repository, requires a TAG, e.g
rake pl:tickets                                       # Make release tickets in JIRA for this project
rake pl:uber_ship                                     # UBER ship: ship all the things in pkg
rake pl:write_build_params                            # Write all package build parameters to a yaml file, pass OUTPUT_DIR to speci...
rake rubocop                                          # run static analysis with rubocop
mckern@flexo katamari (git:master) $ 

```
