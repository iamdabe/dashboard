# Dashboard
This repo holds my personal setup for [gethomepage.dev](https://gethomepage.dev/) for my dashboard start page which lists all my self-hosted services.

## Contents
- `custom.css` - custom css to change the default look
- `services.yaml` – all the apps and services shown
- `settings.yaml` – config and service layout

## Preview
<img src="http://github.com/iamdabe/dashboard/blob/main/screenshot.png?raw=true" alt="Dashboard Screenshot" width="600">

## Notes
- `services.yaml` – where a customapi has been used I've redacted the address but I've kept the path so you should just be able to insert your server ip and you're good to go. The customapis i've used are as follows:

```
# Invoice Shelf
widget:
  type: customapi
  url: https:///api/v1/dashboard
  refreshInterval: 3600000 # Refresh every 1hr
  method: GET
  headers:
    Authorization: Bearer KEY
  display: block
  mappings:
    - field: total_amount_due
      label: Due
      format: currency
      scale: 0.01
      suffix: "€"
    - field: total_invoice_count
      label: Invoices
      format: number


# Lube Logger
widgets:
  - type: customapi
    url: http:///api/vehicle/info/
    refreshInterval: 3600000 # Refresh every 1hr
    method: GET
    display: list
    mappings:
      - field: 
          0: 
            vehicleData: make
        additionalField:
          field:
            0: 
              vehicleData: model
        label: Make
      - field: 
          0: 
            nextReminder: description
        additionalField:
          field: 
            0: 
              nextReminder: dueDate
        label: Reminder
      - field: 
          0: 
            lastReportedOdometer
        suffix: " km"
        label: Odometer

# Grocy
widgets:
  - type: customapi
    url: http:///api/stock
    refreshInterval: 3600000 # Refresh every 1hr
    method: GET
    display: block
    mappings:
      - field:
          0:
            product: name 
        label: Item
      - field:
          0:
            amount
        suffix: " bags"
        label: Intentory

# WatchYourLan
widget:
  type: customapi
  url: http:///api/status/
  refreshInterval: 3600000 # Refresh every 1hr
  method: GET
  display: block
  mappings:
    - field: Known
      label: Known
      format: number
    - field: Unknown
      format: number
      label: Unknown
```
 
## Tools 
- Homepage - [gethomepage.dev](https://gethomepage.dev/) 
- Docker
