# SmartLock

[![N|Solid](http://www.devdigital.com/themes/devdigital2015/images/logo.png)](http://devdigital.com/)

By integrating Smart Lock into your android app, you can automatically sign users in to your app using the credentials they have saved.

## About SmartLock Library
 - Google or, more specifically, Chrome has had a makeshift password manager for a while now. You’ve probably seen it before: any time you enter a password into a site, Chrome will ask if you want to save that password for later. this feature was little more than a slightly fancier version of saying “Keep me logged in” on web sites.

 - Now, the whole system has been upgraded and rolled into Google’s Smart Lock feature. If that name sounds familiar, it’s probably because you’ve used it on your Android(Oreo) phone.

## Why use SmartLock Library?
- Integrate Smart Lock for Passwords into your app by using the Credentials API to retrieve saved credentials on sign-in. Use successfully retrieved credentials to sign the user in, or use the Credentials API to rapidly on-board new users by partially completing your app's sign in or sign up form. Prompt users after sign-in or sign-up to store their credentials for future automatic authentication.

### Requirements
- SmartLock Library can be included in any Android application.
- SmartLock Library supports Android 4.4 and later.
- Add this in your build.gradle
           	
        implementation 'com.devdigital:smartlock:1.0.0'
        
- Then initialize it in onCreate() Method of activity class :
            	
        public class LoginActivity extends AppCompatActivity implements SmartLockManager.CredentialListener {
            //Declare SmartLockManager filed
            private SmartLockManager mPasswordLockManager;

            @Override
            protected void onCreate(Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
               
                //Initialize SmartLockManager
                mPasswordLockManager = new SmartLockManager(this);
                mPasswordLockManager.setCredentialListener(this);

                //Retrieve Credential
                mPasswordLockManager.getCredentialsAsync();	
            }
        
            private void onLoginButtonClick() {
                String email = ...
                String password = ...

                //Save new credential
                mPasswordLockManager.saveCredentials(getString(R.string.app_name), email, password);
            }
        
            @Override
            protected void onActivityResult(int requestCode, int resultCode, Intent data) {
                super.onActivityResult(requestCode, resultCode, data);
                //Call onActivityResult to handle Retrieve/Save credential result 
                mPasswordLockManager.onActivityResult(requestCode, resultCode, data);
            }
        
            @Override
            public void onCredential(Credential credential) {
                mEmailEt.setText(credential.getId());
                mPasswordEt.setText(credential.getPassword());
            }
        }
        
        
