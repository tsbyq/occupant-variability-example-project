
# Load in the rake tasks from the base openstudio-extension gem
require 'openstudio/extension/rake_task'
require 'openstudio/occupant_variability'


module OccupantVariabilityTest
  module TestProject
    class TestProject < OpenStudio::Extension::Extension

      def initialize
        super
        @root_dir = File.absolute_path(File.dirname(__FILE__))
      end

      # Return the absolute path of the measures or nil if there is none, can be used when configuring OSWs
      def measures_dir
        nil
      end

      # Relevant files such as weather data, design days, etc.
      # Return the absolute path of the files or nil if there is none, used when configuring OSWs
      def files_dir
        return File.absolute_path(File.join(@root_dir, 'files'))
      end

    end
  end
end

# Load in the rake tasks from the base extension gem
rake_task = OpenStudio::Extension::RakeTask.new
rake_task.set_extension_class(OccupantVariabilityTest::TestProject::TestProject)


# User defined tasks
desc 'Try to run some tests'
task :run_test do
  puts '~~ This is a test rake task...'

  model_creator =  OpenStudio::OccupantVariability::ModelCreator.new('Test Model',
                                                                     'SmallOfficeDetailed',
                                                                     '90.1-2013',
                                                                     'ASHRAE 169-2006-5A',
                                                                     'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620')
  model_creator.generate_prototype_model()


end

task :run_all => [:run_test]


task default: :run_all