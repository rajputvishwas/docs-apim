# Overriding Developer Portal Theme

WSO2 provides the developers with an easier approach to customize the UI. You do not need to have React, CSS, or HTML knowledge to customize the UI. We have a single JSON file which holds the parameterized constraints of the look and feel. For example, you can change the font family via the JSON file so that the changes appear through out the Developer Portal. When updating the Developer Portal theme, you can update not only the look and feel, but also behaviors such as making the listing view default instead of grid view, hiding social features, etc. 

## Overriding the default theme

The default theme is located in the `<API-M_HOME>/repository/deployment/server/jaggeryapps/devportal/site/public/theme/` directory. 

The `defaultTheme.js` file has all the parameters defining the look and feel of the Developer Portal.

Make sure to take a backup of the `defaultTheme.js` before making any changes.

Changes done in the `defaultTheme.js` file are reflected directly in the Developer Portal ( It's not required to restart the server or rebuild the source code).

## Uploading via the Admin Portal (Tenants Only)

**If you do not have access to the file system** , you can upload the theme via the Admin Portal as shown below:

1.  Download the sample theme here [sampleTheme.zip]({{base_path}}/assets/attachments/Learn/sampleTheme.zip). 
2.  The `sampleTheme.zip` file contains the following folder structure. 

     You can make the changes required to `defaultTheme.json` file and archive it back. The name of the archive does not matter, but the name of the JSON file (`defaultTheme.json`) does.
     
      ```
      ├── css
      │   └── custom.css
      ├── defaultTheme.json
      └── images
          └── custom-logo.png
      ```

3.  Sign in to the WSO2 Admin Portal ([https://server-host:9443/admin](https://server-host:9443/admin)) with your tenant username (format `<username>@<domain>.com kim@testorg.com`) and password.

4.  Expand the **Settings** menu, click **Upload Tenant Theme** and upload your ZIP file. 

    ![Upload tenant theme]({{base_path}}/assets/img/Learn/upload-tenant-theme.png)

5.  Access the API Developer Portal (`https://<server-host>:9443/devportal`) using your tenant username and password.

    Note the new theme is applied.

## Adding custom logo for the tenant

In your tenant theme, you can refer to an image from the `defaultTheme.json` file as follows. The examples below uses the `custom-logo.png` image from the `sampleTheme.zip`. The image can be referred using one of the following URL patterns.

The path format to the `custom-logo.png` image within the tenant domain theme is as follows:

```js
"logo": "/site/public/tenant_themes/<tenant-domain>/images/custom-logo.png",
```
The path to the `custom-logo.png` image within the `kim@testorg.com` tenant domain theme is as follows:

```js
"logo": "/site/public/tenant_themes/kim@testorg.com/images/custom-logo.png",
```

The following defines the logo image from an external URL.

```js
"logo": "https://dummyimage.com/208x19/66aad1/ffffff&text=testlogo",
```

## Applying CSS rules to change the look and feel

If you prefer to change the styling using CSS rules, you can use the `custom.css` file. The above sample theme also has a custom CSS file. In the CSS file, let's change the top header background color to black. 

Note that we have injected IDs into the dom elements. You can use them to apply CSS rules. However, be aware about the dynamically generated CSS class names. These class names have a number suffix which changes from version to version. Therefore, it is recommended not to use them for styling purposes. 

The CSS file is referenced in the `defaultTheme.json` in the following manner. It is not a must to replace the `<tenant-domain> ` in the following line, as at runtime the Developer Portal will automatically replace it with the current tenant domain.

```js
   "tenantCustomCss": "/site/public/tenant_themes/<tenant-domain>/css/custom.css",
```

## Content of defaultTheme.json

```js
{
  "themes": {
    "light": {
      "palette": {
        "primary": {
          "main": "#15b8cf"
        },
        "secondary": {
          "light": "#347eff",
          "main": "#415a85",
          "contrastText": "#ffcc00"
        },
        "background": {
          "default": "#efefef",
          "paper": "#ffffff",
          "drawer": "#1a1f2f"
        }
      },
      "typography": {
        "fontFamily": "\"Open Sans\", \"Helvetica\", \"Arial\", sans-serif",
        "fontSize": 12,
        "body2": {
          "lineHeight": 2
        }
      },
      "custom": {
        "tenantCustomCss": "/site/public/tenant_themes/<tenant-domain>/css/custom.css",
        "contentAreaWidth": 1240,
        "backgroundImage": "",
        "defaultApiView": "list",
        "page": {
          "style": "fluid",
          "width": 1240,
          "emptyAreadBackground": "#1e2129",
          "border": "none"
        },
        "appBar": {
          "logo": "/site/public/tenant_themes/<tenant-domain>/images/custom-logo.png",
          "logoHeight": 34,
          "logoWidth": 128,
          "background": "#1d344f",
          "activeBackground": "#254061",
          "showSearch": true,
          "drawerWidth": 200
        },
        "leftMenu": {
          "position": "vertical-left",
          "style": "icon left",
          "iconSize": 24,
          "leftMenuTextStyle": "uppercase",
          "width": 180,
          "background": "#1a1f2f",
          "leftMenuActive": "#254061",
          "activeBackground": "rgb(29, 52, 79)",
          "rootIconVisible": true,
          "rootIconSize": 42,
          "rootIconTextVisible": false,
          "rootBackground": "#204d6a"
        },
        "infoBar": {
          "height": 70,
          "background": "#ffffff",
          "showBackIcon": true,
          "showThumbnail": true,
          "starColor": "#f6bf21",
          "sliderBackground": "#ffffff",
          "iconOddColor": "#347eff",
          "iconEvenColor": "#89b4ff",
          "listGridSelectedColor": "#347eff",
          "tagChipBackground": "#7dd7f5"
        },
        "listView": {
          "tableHeadBackground": "#fff",
          "tableBodyOddBackgrund": "#efefef",
          "tableBodyEvenBackgrund": "#fff"
        },
        "overview": {
          "titleIconColor": "#89b4ff",
          "titleIconSize": 16
        },
        "adminRole": "admin",
        "commentsLimit": 5,
        "maxCommentLength": 512,
        "overviewPage": {
          "commentsBackground": "/site/public/images/overview/comments.svg",
          "documentsBackground": "/site/public/images/overview/documents.svg",
          "credentialsBackground": "/site/public/images/overview/credentials.svg"
        },
        "resourceChipColors": {
          "get": "#02a8f4",
          "post": "#8ac149",
          "put": "#ff9700",
          "delete": "#fd5621",
          "options": "#5f7c8a",
          "patch": "#785446",
          "head": "#785446"
        },
        "operationChipColor": {
          "query": "#b3e6fe",
          "mutation": "#c1dea0",
          "subscription": "#ffcc80"
        },
        "thumbnail": {
          "width": 240,
          "contentPictureOverlap": false,
          "iconColor": "rgba(0, 0, 0, 0.38)",
          "listViewIconSize": 20,
          "contentBackgroundColor": "rgba(239, 239, 239, 0.5)",
          "defaultApiImage": false,
          "backgrounds": [
            {
              "prime": 2406206207,
              "sub": 1338177791
            },
            {
              "prime": 4101969663,
              "sub": 3453762047
            },
            {
              "prime": 4097980159,
              "sub": 4274063359
            },
            {
              "prime": 563540991,
              "sub": 2934571263
            },
            {
              "prime": 4288086271,
              "sub": 4293606655
            },
            {
              "prime": 4288086271,
              "sub": 4267123455
            }
          ],
          "document": {
            "icon": "library_books",
            "backgrounds": {
              "prime": 3489136639,
              "sub": 3808425983
            }
          }
        },
        "noApiImage": "/site/public/images/nodata.svg",
        "landingPage": {
          "active": false,
          "carousel": {
            "active": true,
            "slides": [
              {
                "src": "/site/public/images/landing/01.jpg",
                "title": "Lorem <span>ipsum</span> dolor sit amet",
                "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer felis lacus, placerat vel condimentum in, porta a urna. Suspendisse dolor diam, vestibulum at molestie dapibus, semper eget ex. Morbi sit amet euismod tortor."
              },
              {
                "src": "/site/public/images/landing/02.jpg",
                "title": "Curabitur <span>malesuada</span> arcu sapien",
                "content": "Curabitur malesuada arcu sapien, suscipit egestas purus efficitur vitae. Etiam vulputate hendrerit venenatis. "
              },
              {
                "src": "/site/public/images/landing/03.jpg",
                "title": "Nam vel ex <span>feugiat</span> nunc laoreet",
                "content": "Nam vel ex feugiat nunc laoreet elementum. Duis sed nibh condimentum, posuere risus a, mollis diam. Vivamus ultricies, augue id pulvinar semper, mauris lorem bibendum urna, eget tincidunt quam ex ut diam."
              }
            ]
          },
          "listByTag": {
            "active": true,
            "content": [
              {
                "tag": "finance",
                "title": "Checkout our Finance APIs",
                "description": "We offers online payment solutions and has more than 123 million customers worldwide. The WSO2 Finane API makes powerful functionality available to developers by exposing various features of our platform. Functionality includes but is not limited to invoice management, transaction processing and account management.",
                "maxCount": 5
              },
              {
                "tag": "weather",
                "title": "Checkout our Weather APIs",
                "description": "We offers online payment solutions and has more than 123 million customers worldwide. The WSO2 Finane API makes powerful functionality available to developers by exposing various features of our platform. Functionality includes but is not limited to invoice management, transaction processing and account management.",
                "maxCount": 5
              }
            ]
          },
          "parallax": {
            "active": true,
            "content": [
              {
                "src": "/site/public/images/landing/parallax1.jpg",
                "title": "Lorem <span>ipsum</span> dolor sit amet",
                "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer felis lacus, placerat vel condimentum in, porta a urna. Suspendisse dolor diam, vestibulum at molestie dapibus, semper eget ex. Morbi sit amet euismod tortor."
              },
              {
                "src": "/site/public/images/landing/parallax2.jpg",
                "title": "Nam vel ex <span>feugiat</span> nunc laoreet",
                "content": "Nam vel ex feugiat nunc laoreet elementum. Duis sed nibh condimentum, posuere risus a, mollis diam. Vivamus ultricies, augue id pulvinar semper, mauris lorem bibendum urna, eget tincidunt quam ex ut diam."
              }
            ]
          }
        },
        "tagWise": {
          "active": false,
          "style": "fixed-left",
          "thumbnail": {
            "width": 150,
            "image": "/site/public/images/api/api-default.png"
          },
          "key": "-group",
          "showAllApis": true
        },
        "tagCloud": {
          "active": true,
          "colorOptions": {
            "luminosity": "light",
            "hue": "blue"
          },
          "leftMenu": {
            "width": 200,
            "height": "calc(100vh - 222px)",
            "background": "#1a1f2f",
            "color": "#c7e9ff",
            "titleBackground": "#335c8b",
            "sliderBackground": "#335c8b",
            "sliderWidth": 25,
            "hasIcon": false
          }
        },
        "social": {
          "showRating": true
        },
        "apiDetailPages": {
          "showCredentials": true,
          "showComments": true,
          "showTryout": true,
          "showDocuments": true,
          "showSdks": true,
          "onlyShowSdks": []
        },
        "banner": {
          "active": false,
          "style": "text",
          "image": "/site/public/images/landing/01.jpg",
          "text": "This is a very important announcement",
          "color": "#ffffff",
          "background": "#e08a00",
          "padding": 20,
          "margin": 0,
          "fontSize": 18,
          "textAlign": "center"
        },
        "footer": {
          "active": true,
          "text": "",
          "background": "#bdbdbd",
          "color": "#222222"
        }
      }
    }
  }
}
```

