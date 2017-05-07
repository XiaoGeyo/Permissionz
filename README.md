# Permissionz
用法：
    1.根目录下的build:
      repositories {
        jcenter()
        maven { url 'https://jitpack.io' }
      }
    
    2.添加依赖:
      compile 'com.github.XiaoGeyo:Permissionz:v2.0'
      
    3.定义请求码:
      static final int REQUEST_CODE = 0; // 请求码
      
    4.初始化:
      mPermissionsChecker = new PermissionsChecker(this);
      
    5.定义权限数组:
      String[] PERMISSIONS = new String[]{
            Manifest.permission.RECORD_AUDIO,//录制音频
            Manifest.permission.MODIFY_AUDIO_SETTINGS,//全局音频
            Manifest.permission.CAMERA//相机
      };
    
    6.onResume()中:
      if (mPermissionsChecker.lacksPermissions(PERMISSIONS)) {
            startPermissionsActivity();
        }
        
    7.
      private void startPermissionsActivity() {
        PermissionsActivity.startActivityForResult(this, REQUEST_CODE, PERMISSIONS);
      }
    
    8.
      @Override
      protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        // 拒绝时, 关闭页面, 缺少主要权限, 无法运行
        if (requestCode == REQUEST_CODE && resultCode == PermissionsActivity.PERMISSIONS_DENIED) {
            finish();
        }else {
            //Intent intent=new Intent(this,Main2Activity.class);
            //startActivity(intent);

        }
    }
