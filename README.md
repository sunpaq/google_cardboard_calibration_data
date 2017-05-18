# google_cardboard_calibration_data
a repo to save some VR viewer datas used to initialize Google VR SDK VRView

### example to use the data on iOS (swift)

        let path = Bundle.main.path(forResource: "cardboard_calibration_data", ofType: "txt")
        let uri = URL.init(fileURLWithPath: path!)
        GVRPanoramaView.setViewerParamsFrom(uri) {
            (success, error) in
            if success {
                print("SET CARDBOARD PARAMETERS SUCCESS")
            } else {
                print(error.debugDescription)
            }
        }
        
        
### how i get the raw data

    1. check the URL below to find whether or not there already have your viewer QR. if have goto step 3
    http://www.hypergridbusiness.com/faq/vr-headset-qr-codes/
    
    2. find the parameters like FOV of your VR viewer on web. then goto Google's profile generator
    fill the parameters (mainly FOV) as required. then you will get an QR code. you can download the image
    https://vr.google.com/cardboard/viewerprofilegenerator/
    
    3. use some QR decoder online or offline to get the raw data and save it in txt file.
    https://zxing.org/w/decode.jspx
    
    4. once you have the raw data. you can read them by code like above example.
    
    
