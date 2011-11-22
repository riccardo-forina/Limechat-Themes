namespace :themes do
  
  desc 'Create symlinks for all of the themes in the current directory'
  task :linkup do
    %x[git submodule init && git submodule update]
    puts "updates done. linkup starting"
    #for some reason this is barfing on the css files. try it later    
    Dir.glob("#{File.dirname(__FILE__)}/**/*.css") { |css|
        newcss = File.basename(css)
        FileUtils.ln_s css, newcss, :force => true
        }
    Dir.glob("#{File.dirname(__FILE__)}/**/*.yaml") { |yaml|
        newyaml = File.basename(yaml)
        FileUtils.ln_s yaml, newyaml, :force => true
        }
    Dir.glob("#{File.dirname(__FILE__)}/**/*.js") { |js|
        newjs = File.basename(js)
        FileUtils.ln_s js, newjs, :force => true
        }
  end

  desc 'Install into the logged in user\'s limechat directory'
  task :install do
    puts "Starting updates"
    %x[git submodule init && git submodule update]
    puts "Moving Files"
    source = Dir.getwd + "/."
    Dir.chdir

    app_support_base = Dir.getwd + '/Library/Application Support'
    target = app_support_base + '/net.limechat.LimeChat-AppStore/Themes/' # app store installation dir
    
    unless File.directory?(target)
      target = app_support_base + '/LimeChat/Themes/'
    end
    
    FileUtils.cp_r(source, target, :remove_destination => true)
      puts "Setting up Symlinks"
      puts "Installing themes into #{target}"
      Dir.chdir(target)  
      Dir.glob("#{File.dirname(__FILE__)}/**/*.css") { |css|
          newcss = File.basename(css)
          FileUtils.ln_s css, newcss, :force => true
          }
      Dir.glob("#{File.dirname(__FILE__)}/**/*.yaml") { |yaml|
          newyaml = File.basename(yaml)
          FileUtils.ln_s yaml, newyaml, :force => true
          }
      Dir.glob("#{File.dirname(__FILE__)}/**/*.js") { |js|
          newjs = File.basename(js)
          FileUtils.ln_s js, newjs, :force => true
          }
  end
  
  desc 'Initalize the directory, loading the submodules'
  task :init do
    %x[git submodule init && git submodule update]
  end
  
  desc 'Update the themes directory'
  task :update do
    %x[git pull && git submodule init && git submodule update]
  end
  
end