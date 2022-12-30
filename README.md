conan create . -c tools.system.package_manager:mode=install -c tools.system.package_manager:sudo=True --profile:build .conan/profiles/gcc12 --profile:host .conan/profiles/gcc12  --build wiresharkDissectorPluginExample &> build.log

cp ~/.conan/data/jupyShark/0.0.1/_/_/package/174df609440df17baf334e1f5953cca909f2ae18/plugins/foo.so .local/lib/wireshark/plugins/4.0/epan/

Launch wireshark
Menu Analyze
Open “Enabled Protocols” menu and filter with "foo" to see your dissector.