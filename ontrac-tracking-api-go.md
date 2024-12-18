OnTrac Tracking API - Go
================================
Use Go to track OnTrac shipments with OnTrac Tracking API.

Features
--------
- Real-time OnTrac tracking.
- Batch OnTrac tracking.
- Other features to manage your OnTrac tracking.

Installation
------------

Installation is easy:

    $ go mod init github.com/my/repo
    $ go get github.com/trackingmore-api/trackingmore-sdk-go

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your OnTrac shipments.

Usage
----------

Create a tracking (Real-time tracking):

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }
      
      params := trackingmore.CreateTrackingParams{
        TrackingNumber: "D10015939090075",
        CourierCode:    "ontrac",
      }      

      result, err := cli.CreateTracking(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Create trackings (Max. 40 tracking numbers create in one call):

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }
      
      params := []trackingmore.CreateTrackingParams{
          {
          TrackingNumber: "C12205259026558",
          CourierCode:    "ontrac",
          },
          {
          TrackingNumber: "D10015659891795",
          CourierCode:    "ontrac",
          },
      }   

      result, err := cli.BatchCreateTrackings(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Get status of the shipment:

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }

      params := trackingmore.GetTrackingResultsParams{
        CreatedDateMin: "2023-08-23T06:00:00+00:00",
        CreatedDateMax: "2023-09-05T07:20:42+00:00",
      }  

      result, err := cli.GetTrackingResults(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Update a tracking by ID:

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }

      params := trackingmore.UpdateTrackingParams{
        CustomerName: "New name",
        Note:         "New tests order note",
      }
      idString := "98d15bc9498de1b168d2c6c4ded37176"
      
      result, err := cli.UpdateTrackingByID(context.Background(), idString, params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }
