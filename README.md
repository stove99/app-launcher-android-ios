# 설치
    npm i app-launcher-android-ios

# 사용법
```javascript
    import * as launcher from 'app-launcher-android-ios';

    launchExternalApp(iosSchemaName: string, androidPackageName: string, httpUrl: string, 
                        httpUrliOS: string, httpUrlAndroid: string) {
        let app: string;

        if (this.isIos()) {
            app = iosSchemaName;
        } else if (this.isAndroid()) {
            app = androidPackageName;
        } else {
            // 일반 브라우져로 open
            // this.iab.create(httpUrl);
            return;
        }

        this.appAvailability.check(app).then(
            () => {
                // 앱 실행
                if (this.isIos()) {
                    launcher.uriLaunch(app);
                }
                else if (this.isAndroid()) {
                    launcher.packageLaunch(app);
                }
            },
            () => {
                // 앱이 없으면 마켓으로 이동
                if (this.isIos()) {
                    this.iab.create(httpUrliOS);
                }
                else if (this.isAndroid()) {
                    this.iab.create(httpUrlAndroid, '_system');
                }
            }
        );
    }
```

# 참고
  - [https://forum.ionicframework.com/t/open-other-app-using-package-id-name/117089](https://forum.ionicframework.com/t/open-other-app-using-package-id-name/117089)
  - 위 사이트 따라하다 js 로 만드니까 typescript 컴파일이 안되서 npm 에 올리는걸로 했음.
