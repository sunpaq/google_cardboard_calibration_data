# google_cardboard_calibration_data

    a repo to save some VR viewer datas used to initialize Google VR SDK VRView on iOS
    instead of scan QR code and send request to Google's Server. the plists can be used offline 
    (someplace can not access Google's server. or simply doesn't have network connection)

### example to use the data on iOS (swift)

    private let kGVRSDK:String = "com.google.cardboard.sdk.DeviceParamsAndTime"

    func loadCardboardParameters(_ filename: String) {
        if let saved = UserDefaults.standard.value(forKey: kGVRSDK) {
            print("GOOGLE CARDBOARD ALREADY SETUP: \(filename)")
            print("DATA: \(saved)")
        } else {
            if let url = Bundle.main.url(forResource: filename, withExtension: "plist") {
                do {
                    let data = try Data(contentsOf:url)
                    let dict = try PropertyListSerialization.propertyList(from: data, options: [], format: nil) as! [String:Any]
                    
                    if let gvrdata = dict[kGVRSDK] {
                        UserDefaults.standard.set(gvrdata, forKey: kGVRSDK)
                        print("SETUP GOOGLE CARDBOARD SUCCESS: \(filename)")
                        print("DATA: \(gvrdata)")
                    }
                    
                } catch {
                    print("SETUP GOOGLE CARDBOARD FAILED: \(filename)")
                    print(error)
                }
            }
        }
    }
        
        
### how i get the raw data

    1. check the URL below to find whether or not there already have your viewer QR. if donesn't goto step 2
    http://www.hypergridbusiness.com/faq/vr-headset-qr-codes/
    
    2. find the parameters like FOV of your VR viewer on web. then goto Google's profile generator
    fill the parameters (mainly FOV) as required. then you will get an QR code. you can download the image
    https://vr.google.com/cardboard/viewerprofilegenerator/
    
    3. open your developing App which is calling Google VR SDK
    goto the left-right side by side view. and type the settings gear button on right top
    scan the QR code
    
    4. keep your App stay on the VR view. then connect your iPhone with Mac.
    open the Xcode. on the top most menu "Window - Devices"
    select your iPhone on Devices list. then select your App on "Installed Apps"
    click the gear button on right bottom of the list
    select "Download Container" and save the data in your folder

    5. open your saved data by right click it then "Show Package Contents"
    'AppData/Library/Preferences/xxxx.plist' is your data.
    double click to open it. and find the key 'com.google.cardboard.sdk.DeviceParamsAndTime'
    delete all the other key-value pairs except this key-value. Google VR SDK will use this data for initialize 

    4. once you have the raw data. you can read them by code like above example.
    
    
