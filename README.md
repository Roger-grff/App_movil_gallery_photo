<img width="363" height="490" alt="WhatsApp Image 2026-04-19 at 20 20 52" src="https://github.com/user-attachments/assets/6cffa241-5154-475f-b0d0-232ad9186e75" />
<img width="1080" height="2340" alt="WhatsApp Image 2026-04-19 at 20 20 52 (1)" src="https://github.com/user-attachments/assets/b9e85482-3536-4938-a9bc-b6491cc3b2ec" />

Teniendo nuestra base principal de la aplicacion nos dirigimos a la documentación de capacitor, especificamente al de @capacitor/splash-screen

insralamos lo siguiente:      

                              npm install @capacitor/splash-screen

y posteriormente agregamos la siguiente linea de ejemplo de codgio de capacitor, luego la pegamos en capacitor.config.ts

                              plugins: {
                                SplashScreen: {
                                  launchShowDuration: 3000,
                                  launchAutoHide: true,
                                  launchFadeOutDuration: 3000,
                                  backgroundColor: "#ffffffff",
                                  androidSplashResourceName: "splash",
                                  androidScaleType: "CENTER_CROP",
                                  showSpinner: true,
                                  androidSpinnerStyle: "large",
                                  iosSpinnerStyle: "small",
                                  spinnerColor: "#999999",
                                  splashFullScreen: true,
                                  splashImmersive: true,
                                  layoutName: "launch_screen",
                                  useDialog: true,
                                },
                              },
                              
y cambiamos lo siguiente:

                         launchShowDuration: 0,    ===> lo modificaemos acontinuacion en el app.components.ts para que en todos los dispositivos funcione
                         showSpinner: false,       ===> desactivamos la animacion de carga
                         splashFullScreen: false,  ===> la desactivamos para que no se vea de fondo
                         splashImmersive: false,   ===> la desactivamos para que no ocupe toda la pantalla
                         useDialog: false,         ===> lo desactivamos para tener mas control 
                         
seguimos con el archivo app.components.ts y agregamos lo siguiente 

                        import { SplashScreen } from '@capacitor/splash-screen'; ===> importamos las liblerias necesarias para el splash
                        async showSplashScreen() {
                          await SplashScreen.show({
                              autoHide: true,      ===> se va a desvanecer el splash
                              showDuration: 3000,  ===> los microsegundos que va a durar el splash
                            });
                          }
                          
y dentro de la clase AppComponent agregamos la funcion this.showSplashScreen(). quedaria de la siguiente forma:

                                    import { Component } from '@angular/core';
                                    import { SplashScreen } from '@capacitor/splash-screen';
                                    @Component({
                                      selector: 'app-root',
                                      templateUrl: 'app.component.html',
                                      styleUrls: ['app.component.scss'],
                                      standalone: false,
                                    })
                                    export class AppComponent {
                                      constructor() {
                                        this.showSplashScreen()
                                      } 
                                      async showSplashScreen() {
                                        await SplashScreen.show({
                                          autoHide: true,
                                          showDuration: 3000,
                                        });
                                      }
                                    }
seguimos con la instalacion de los componentes para android con 

                                    npm i @capacitor/android 

seguimos para agregar la plataforma de android con 

                                    npx cap add android

seguimos con la guia de capacitor docs en Splash Screen and Icons e instalamos lo necesario usando @capacitor/assets con el siguiente codigo 

                                  npm i @capacitor/assets 

posteriormente creamos una nueva carpeta llamada assets en la raiz del proyecto y agregamos nuestra imagen del icono y del splasher con las medidas 
que nos solicita la guia y con los nombres especificos "icon.png" y "splash.png"

luego para generar las imagenes seguimos con el siguiente comando 

                                  npx capacitor-assets generate
                                  
esto nos genera los recursos para que se cree el icono y el splash en diferentes resoluciones
seguimos con con la generacino del apk guardando todo los cambion con 

                                  ionic cap copy
                                  ionic cap sync

y para abrirlo con el android studio usamos: 

                                  ionic cap open android
                                    
en android estudio generamos el apk
por ultimo personalisamos la correcta se ajuste adecuadamente en versiones de android anteriores modificamos el archivo styles.xml en la direccion 
android/app/scr/main/res/values/style.xml y modificamos el codigo 

                                <style name="AppTheme.NoActionBarLaunch" parent="Theme.SplashScreen"> 
                                                                por   
                                <style name="AppTheme.NoActionBarLaunch" parent="AppTheme.NoActionBar">
y eso seria todo !! 

video de sugerencia: https://www.youtube.com/watch?v=WW11WQVuS8s
