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
        
        
