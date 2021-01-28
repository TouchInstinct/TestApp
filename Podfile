source 'https://cdn.cocoapods.org/'
source 'https://github.com/TouchInstinct/Podspecs.git'

platform :ios, '12.0'

use_frameworks!
inhibit_all_warnings!

project 'testapp', {
    'AppStore' => :release,
    'Release' => :release,
    'Debug' => :debug
}

target 'testapp' do

  # System
  pod 'SwiftLint'
  pod 'LicensePlist'
  pod 'Firebase/Crashlytics'
  pod 'Firebase/Performance'
  pod 'Firebase/Analytics' # for Firebase/Performance

end

# fixes Xcode 12 warnings:
# "The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.0.99."
# see https://github.com/CocoaPods/CocoaPods/issues/9884

min_supported_deployment_target = Version.new(9.0) # as of Xcode 12

post_install do |pi|
  pi.pods_project.targets.each do |target|
     target.build_configurations.each do |config|
      build_config_version = Version.new(config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'])
      max_deployment_target = [build_config_version, min_supported_deployment_target].max

      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = max_deployment_target.to_s
    end
  end
end

# If you have slow HDD
ENV['COCOAPODS_DISABLE_STATS'] = "true"
