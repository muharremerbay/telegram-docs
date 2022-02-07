# Tebaş Otomasyon API Service

`Tebaş Otomasyon - Telegram API servis dökümantasyonu`

### Kullanım
API BASE URL  =>  `https://api.tebasonline.com`
```
    > Tüm isteklerde "headers" alanında `telegram-api-key` ve `telegram-api-secret` gönderilmesi zorunludur.
```

# Projeler
`Tebaş Enerjinin okuma ve paylaşımını yaptığı projelerin listesi`

| Route | HTTP Verb	| Request Body | Result Data | Description	 |
| --- | --- | --- | --- | --- |
| /telegram/all-projects | `GET` | NULL | `Type: Array, Data Description: Project List` | ` Geriye dönen data Array tipinde veri tabanına eklenmiş tüm projelerin listesi olacaktır.`|

### Örnek Sonuç
```
{
    "code": 200,
    "data": {
        "projects": [
            {
                "blocks": [
                    {
                        "_id": "xxxxxxxx",
                        "name": "A BLOK"
                    }
                ],
                "_id": "xxxxxxxx",
                "name": "KADİR APARTMANI",
                "city": {
                    "_id": "xxxxxxxx",
                    "name": "İSTANBUL"
                }
            },
            {
                "blocks": [
                    {
                        "_id": "xxxxxxxx",
                        "name": "B BLOK"
                    },
                    {
                        "_id": "xxxxxxxx",
                        "name": "C BLOK"
                    }
                ],
                "_id": "xxxxxxxx",
                "name": "EKŞİOĞLU SİTESİ",
                "city": {
                    "_id": "xxxxxxxx",
                    "name": "MALATYA"
                }
            }
        ]
    }
}
```

# Sayaçlar
`Tebaş Enerjinin okuma ve paylaşımını yaptığı projelerin sayaçları`

| Route | HTTP Verb	| Request Body | Result Data | Description	 |
| --- | --- | --- | --- | --- |
| /telegram/block-counters | `GET` | { project: ID, blocks:[ID, ID, ID, ID, ID] }| `Type: Array, Data Description: Counter List` | ` Geriye dönen data Array tipinde göndermiş olduğunuz bloklara ait sayaç listesi olacaktır.`|

### Örnek Request
```
/telegram/block-counters?blocks=1&blocks=2&blocks=3&blocks=4&project=asd123
```
### Örnek Sonuç
```
{
    "code": 200,
    "data": {
        "apartmentCounters": [
            {
                "counterDatas": null,
                "_id": "xxxxxxxxx",
                "apartment": {
                    "squareMeters": 0,
                    "_id": "xxxxxxxxx",
                    "name": "A-01",
                    "block": {
                        "_id": "xxxxxxxxx",
                        "name": "A BLOK  2"
                    }
                },
                "serialNumber": "010101101919191991919191",
                "type": {
                    "_id": "xxxxxxxxx",
                    "name": "Isıtma Kalorimetre"
                },
                "lastClosedData": [
                    {
                        "periodDescription": "sayaçta su kaçağı tespit edildi",
                        "_id": "6124b4fc34477b3bfd65a3d9",
                        "counterValue": 999999
                    }
                ],
                "id": "xxxxxxxxx"
            },
            {
                "counterDatas": null,
                "_id": "xxxxxxxxx",
                "apartment": {
                    "squareMeters": 67.88,
                    "_id": "xxxxxxxxx",
                    "name": "D-KREŞ 02",
                    "block": {
                        "_id": "xxxxxxxxx",
                        "name": "TEST B"
                    }
                },
                "type": {
                    "_id": "xxxxxxxxx",
                    "name": "Isıtma Kalorimetre"
                },
                "serialNumber": "115115002043",
                "lastClosedData": [
                    {
                        "periodDescription": "",
                        "_id": "6124b4fc34477b3bfd65a3a1",
                        "counterValue": 999999
                    }
                ],
                "id": "xxxxxxxxx"
            }
        ]
    }
}
```

# Sayaç Verileri
`Tebaş Enerjinin okuma ve paylaşımını yaptığı sayaçların verileri`

| Route | HTTP Verb	| Request Body | Result Data | Description	 |
| --- | --- | --- | --- | --- |
| /telegram/add-new-data | `POST` | { project: ID, serialNumber: Int, counterValue: Double, periodDescription: String }| `Type: Array, Data Description: Created Counter Period Value` | ` Geriye dönen data Obje tipinde göndermiş olduğunuz bilgilere ait sayaca eklenmiş dönem verisi olacaktır.`|

### Örnek Request
```
/telegram/add-new-data
```
### Örnek Request Body
```
{
    project: 123,
    serialNumber: 123,
    counterValue: 123,
    periodDescription: "Sayacın mbus kablosu kopuk"
}
```
### Örnek Sonuç
```
{
    "code": 200,
    "apartmentCounterData": {
        "oldCounterValue": 999999,
        "periodDescription": "Sayacın mbus kablosu kopuk",
        "periodConsumption": 9000000,
        "dataStatus": 0,
        "turnoverStatus": false,
        "turnoverConsumption": 0,
        "takenoverConsumption": 0,
        "problemState": false,
        "analysisStatus": false,
        "comparisonMakingStatus": false,
        "fifteenDegreesProblem": false,
        "fifteenDegreesValue": 0,
        "minusConsumptionProblem": false,
        "maximumConsumptionProblem": false,
        "lastThreeMonthProblem": false,
        "undefinedEndexProblem": false,
        "dataResetStatus": false,
        "_id": "123",
        "counter": "123",
        "period": "123",
        "counterValue": 9999999,
        "createdAt": "2022-02-07T08:20:03.234Z",
        "__v": 0
    }
}
```