
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



desc 'Check configurations'
task :run_check do
  puts '~~~ Check configurations...'

  occ_var = OpenStudio::OccupantVariability::OccupantVariability.new()

  puts "Root dir = #{occ_var.root_dir}"
  puts "Measure dir = #{occ_var.measures_dir}"
  puts "File dir = #{occ_var.files_dir}"
  puts "Doc templates dir = #{occ_var.doc_templates_dir}"
  puts "Core dir = #{occ_var.core_dir}"

end


# User defined tasks
desc 'Try to create model from openstudio-standards'
task :run_create_model_test do
  puts '~~~ Try to create model from openstudio-standards...'

  model_creator =  OpenStudio::OccupantVariability::ModelCreator.new('Test Model',
                                                                     'SmallOfficeDetailed',
                                                                     '90.1-2013',
                                                                     'ASHRAE 169-2006-5A',
                                                                     'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620')
  model_creator.generate_prototype_model()


end


desc 'Try to apply occupancy simulator measure'
  task :run_apply_occupancy_simulator do
    puts '~~~ Try to apply occupancy simulator measure...'
    occ_var_ext = OpenStudio::OccupantVariability::Extension.new
    baseline_osw_dir = occ_var_ext.files_dir
    files_dir = occ_var_ext.files_dir
    apply_occ_sim = OpenStudio::OccupantVariability::OccupancySimulatorApplier.new(baseline_osw_dir, files_dir)

    seed_file_dir = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620/TestModel.osm'
    weather_file_dir = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620/TestModel.epw'
    run_dir = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620/rundir'

    osw = apply_occ_sim.create_osw(seed_file_dir, weather_file_dir)

    puts osw

    runner = OpenStudio::Extension::Runner.new()
    runner.run_osw(osw, run_dir)


  end


desc 'Try to apply occupancy variability LOD2'
task :run_apply_LOD2 do
  puts '~~~ Try to apply occupancy variability LOD2 measures...'
  occ_var_ext = OpenStudio::OccupantVariability::Extension.new
  baseline_osw_dir = occ_var_ext.files_dir
  files_dir = occ_var_ext.files_dir
  apply_occ_sim = OpenStudio::OccupantVariability::OccupancySimulatorApplier.new(baseline_osw_dir, files_dir)

  # Use relative path
  seed_file_dir = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620/TestModel.osm'
  weather_file_dir = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620/TestModel.epw'
  run_dir = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/Test_Demonstration/620/rundir'

  occ_sch_path = 'E:/Users/Han/Documents/GitHub/OpenStudio_related/openstudio-occupant-variability-gem/lib/files/OccSimulator_out_IDF.csv'

  osw = apply_occ_sim.create_osw(seed_file_dir, weather_file_dir, 2, occ_sch_path, occ_sch_path)

  puts osw

  runner = OpenStudio::Extension::Runner.new()
  runner.run_osw(osw, run_dir)


end



task :run_all => [:run_create_model_test]
task default: :run_all