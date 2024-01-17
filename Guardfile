# A sample Guardfile
# More info at https://github.com/guard/guard#readme

## Uncomment and set this to only include directories you want to watch
# directories %w(app lib config test spec features) \
#  .select{|d| Dir.exist?(d) ? d : UI.warning("Directory #{d} does not exist")}

## Note: if you are using the `directories` clause above and you are not
## watching the project directory ('.'), then you will want to move
## the Guardfile to a watched dir and symlink it back, e.g.
#
#  $ mkdir config
#  $ mv Guardfile config/
#  $ ln -s config/Guardfile .
#
# and, you'll have to watch "config/Guardfile" instead of "Guardfile"

# Guardのマッチング規則を定義
guard :minitest, cmd: "bin/rails test", all_on_start: false do
  watch(%r{^test/(.*)/?(.*)_test\.rb$})
  watch('test/test_helper.rb') { 'test' }
  watch('config/routes.rb')    { 'test/routing' }
  watch('app/controllers/application_controller.rb') { 'test/controllers' }
  watch(%r{^app/(.+)/?(.*)_controller.rb$}) { |m| "test/#{m[1]}/#{m[2]}_controller_test.rb" }
  watch('app/channels/application_cable/connection.rb') { 'test/channels' }
  watch(%r{^app/(.*)(\.erb|\.haml|\.slim)$}) { |m| "test/#{m[1]}#{m[2]}_test.rb" }
  watch(%r{^lib/(.*)\.rb$}) { |m| "test/lib/#{m[1]}_test.rb" }
  watch(%r{^test/.+_test\.rb$})
end

# 与えられたリソースに対応する統合テストを返す
def integration_tests(resource = :all)
    if resource == :all
        Dir["test/integration/*"]  else
        Dir["test/integration/#{resource}_*.rb"]
    end
end

# 与えられたリソースに対応するコントローラのテストを返す
def controller_test(resource)
    "test/controllers/#{resource}_controller_test.rb"
end

# 与えられたリソースに対応するすべてのテストを返す
def resource_tests(resource)
    integration_tests(resource) << controller_test(resource)
end
