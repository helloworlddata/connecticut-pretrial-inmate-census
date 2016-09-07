require 'pathname'
require 'date'

DATA_DIR = Pathname 'catalog'
WRANGLE_DIR = Pathname 'wrangle'
CORRAL_DIR = WRANGLE_DIR / 'corral'
SCRIPTS = WRANGLE_DIR / 'scripts'
DIRS = {
    'fetched' => CORRAL_DIR / 'fetched',
    'published' => DATA_DIR,
}




desc 'Setup the directories'
task :setup do
    DIRS.each_value do |p|
        unless p.exist?
            p.mkpath()
            puts "Created directory: #{p}"
        end
    end
end


desc "Fetch and timestamp"
task :fetch  => [:setup] do
  todaystr = Date.today.to_s
  destpath = DIRS['fetched'] / "#{todaystr}.csv"
  sh %Q{
curl -o #{destpath} \
 'https://data.ct.gov/api/views/b674-jy6w/rows.csv?accessType=DOWNLOAD'
  }
end

# desc "Compile everything"
# task :compile  => [:setup] do
#   C_FILES.each_value{|fn| Rake::Task[fn].execute() }
# end

# desc "publish everything"
# task :publish  => [:setup] do
#   P_FILES.each_value{|fn| Rake::Task[fn].execute() }
# end
