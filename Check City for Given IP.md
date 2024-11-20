import requests
url="https://ipinfo.io/154.80.70.224/geo"

response = requests.get(url)
mydata=response.json()
for key,value in mydata.items():
    if key=="city" and value=="Islamabad":
        print(f"Yes {value} is here")
