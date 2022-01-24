```
# Uncomment the next line to define a global platform for your project
platform :ios, '9.0'

# 多个target公用的三方这么写
abstract_target 'CommonPods' do

    pod 'AFNetworking', '~> 3.2.1'

    #为单个target单独配置三方
    target 'driver' do
      # use_frameworks!
        pod 'OC_CWCarousel', '~> 1.1.3'
    end

    #为单个target单独配置三方
    target 'manager' do
      # use_frameworks!
        pod 'Masonry', '~> 1.1.0'
    end

end
```

