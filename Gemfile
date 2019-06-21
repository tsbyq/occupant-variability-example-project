source "http://rubygems.org"

# Allow local for developing
allow_local = true

occupant_variability_gam_dir = '../openstudio-occupant-variability-gem'
occupant_variability_gam_dir = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/openstudio-occupant-variability-gem'


if allow_local && File.exists?('../OpenStudio-extension-gem')
  # gem 'openstudio-extension', github: 'NREL/OpenStudio-extension-gem', branch: 'develop'
  gem 'openstudio-extension', path: '../OpenStudio-extension-gem'
else
  gem 'openstudio-extension', github: 'NREL/OpenStudio-extension-gem', branch: 'develop'
end

if allow_local && File.exist?(occupant_variability_gam_dir)
  gem 'openstudio-occupant-variability', path: occupant_variability_gam_dir
else
  gem 'openstudio-occupant-variability', github: 'tsbyq/openstudio-occupant-variability-gem', branch: 'master'
end

# gem 'openstudio-standards', '0.2.9' # doesn't work in 0.2.8?
# Use development
# gem 'openstudio-standards', github: 'NREL/openstudio-standards', branch: 'master'

# simplecov has an unneccesary dependency on native json gem, use fork that does not require this
gem 'simplecov', github: 'NREL/simplecov'