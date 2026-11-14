# Truck ban feed

`bans.json` is downloaded by the app (`BanDataStore.feedURL`) every 12 hours. It holds only what national
law leaves to yearly decrees; weekly rules live in `KabinaCore/TruckBans.swift`, and public holidays come
from Nager.Date.

Per country (ISO code), all optional:

- `windows`: extra ban periods, local time of the country, `"yyyy-MM-dd HH:mm"`; `partial: true` when only
  some roads or regions are affected. Examples: French summer Saturdays, Italian decree Fridays and Saturdays.
- `free`: days (`"yyyy-MM-dd"`) when the weekly rules do not apply, for a lifted ban.
- `holidays`: `{"2027": ["2027-01-01", …]}` replaces the holiday list for that year.

```json
{"version": 1, "updated": "2027-06-01", "countries": {
  "FR": {"windows": [{"from": "2027-07-10 07:00", "to": "2027-07-10 19:00"}]},
  "IT": {"windows": [{"from": "2027-07-23 16:00", "to": "2027-07-23 22:00"}]}
}}
```

Publish by copying `bans.json` to the public repo `kossless/tacho-pilot-feeds` (branch `main`) and pushing.
Check the result with `cd Packages/KabinaCore && swift test` and a decode of the file before publishing.
