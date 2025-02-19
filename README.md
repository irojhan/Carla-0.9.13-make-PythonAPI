# Carla 0.9.13 Update.bat, make PythonAPI Errors solutions
After cloning required verion of Carla simulator, you may face the following errors:
1. Update.bat error: this error cause due to broken link in "update batch" file. to resolve this issue you can download carla package from this [link](http://carla-assets.s3.us-east-005.backblazeb2.com/20211112_d5cfa12.tar.gz):
   * Extract the assets in Unreal\CarlaUE4\Content\Carla. If the path doesn't exist, create it.
   * after this manual modification, there is no need to run Update.bat

2. make PythonAPI error: in this step you may face a lot of errors. to prevent these issues just simply do the following modifications:
   1. Replace the broken link in <path-to-carla>\Util\InstallersWin\install_zlib.bat
      # line 57
      set ZLIB_REPO=http://www.zlib.net/zlib%ZLIB_VERSION:.=%.zip
      # replace with this
      set ZLIB_REPO=https://github.com/madler/zlib/archive/refs/tags/v%ZLIB_VERSION%.zip

   2. Download backup boost zip file (‘boost_1_72_0.zip’) with this [link](https://carla-releases.s3.us-east-005.backblazeb2.com/Backup/boost_1_72_0.zip) to carla/Build directory.
   3. Download source code and extract content to <path-to-carla>\Build\xerces-c-3.2.4-source (make sure to download and rename version from 3.2.3 to 3.2.4):
      1. https://archive.apache.org/dist/xerces/c/3/sources/xerces-c-3.2.4.zip
      2. rename line 103 and 104 in <path-to-carla>\Utils\BuildTools\BuildOSM2ODR.bat to :
          * -DXercesC_INCLUDE_DIR=%INSTALLATION_DIR:/=\%\xerces-c-3.2.4-install\include^
          * -DXercesC_LIBRARY=%INSTALLATION_DIR:/=\%\xerces-c-3.2.4-install\lib\xerces-c.lib^
      3. rename line 43 in <path-to-carla>\Util\InstallersWin\install_xercesc.bat to:
          * set XERCESC_VERSION=3.2.4

    4. in some cases, BuildPythonAPI.bat will find the incorrect python version to run this batch file. to prevent occuring its error, just simply modify the following line(112) of code in <path-to-carla>\Utils\BuildTools\BuildPythonAPI.bat to: specify the directory of required python version
          * "C:\Users\hi3334\AppData\Local\Programs\Python\Python37\python.exe" setup.py bdist_egg bdist_wheel
      
  ## Last Step ##
   3. It seems like Xerces can't be installed properly, here is the solution for it.
      1. Install Xerces by conda install -c anaconda xerces-c
      2. Then find Anaconda3 folder, copy-paste everything from Anaconda3\pkgs\xerces-c-3.2.4-ha925a31_0\Library to carla\Build\xerces-c-3.2.4-install.
      3. Next, copy-paste file xerces-c_3.lib from carla\Build\xerces-c-3.2.4-install\lib to folder carla\PythonAPI\carla\dependencies\lib

then make PythonAPI.
# You can find modified files in this repository. Enjoy
