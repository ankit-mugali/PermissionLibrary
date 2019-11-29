# PermissionLibrary
This library is for getting the permission from user to run the android feature in app.
To use this library you have to download and add in your current project and in Main/Permission activity implement PermissionResultcallback and OnRequestPermissionsResultCallback and import there respective method.

Then Main/Permission activity, add below codes, 

PermissionUtils permissionUtils;

ArrayList<String> permissions = new ArrayList<>();


    public void check_permission() {
        try {
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
                permissionUtils = new PermissionUtils(MainActivity.this);

            permissions.add(Manifest.permission.WRITE_EXTERNAL_STORAGE);
            permissions.add(Manifest.permission.CAMERA);
            permissions.add(Manifest.permission.READ_EXTERNAL_STORAGE);
            permissionUtils.check_permission(permissions, "To use CAMERA " + "requires Permissions", 1);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
Just add as many as permission you want in abpve array and in your manifest file.

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions,
                                           @NonNull int[] grantResults) {
        permissionUtils.onRequestPermissionsResult(requestCode, permissions, grantResults);
        switch (requestCode) {
            case 1: {
                // If request is cancelled, the result arrays are empty.
                if (grantResults.length > 0
                        && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    // check_permission was granted, yay! Do the
                    // contacts-related task you need to do.
                } else {
                    // check_permission denied, boo! Disable the
                    // functionality that depends on this check_permission.
                  }
                return;
            }
        }
    }
