# FAQ

### Is GridPrice free?

Yes. The website, the API and the cards are free, with no account and no API key. The Android app is free in beta.

### Is this my actual electricity rate?

It is the part of your rate that changes through the day. ComEd and Ameren show the hourly supply price their hourly-pricing customers pay. Elsewhere it is the grid operator's real-time wholesale price for your zone. Your bill adds delivery, taxes and fees, which stay the same whatever the hour. See [what these prices are](coverage.md#what-these-prices-are).

### Why would I care if I'm on a fixed rate?

On a fixed rate the hourly price does not change what you pay this month. It is still worth knowing if you are deciding whether to switch to an hourly or time-of-use plan, if you run a battery or solar, or if you just want to use power when the grid is least strained, which is usually when it is cleanest too.

### Why is the price sometimes negative?

When there is more wind or solar on the grid than it can use, wholesale prices drop below zero. It happens in Texas, the plains and California, usually around midday or on windy nights. For anyone whose plan follows wholesale prices, that is the best time to run the dishwasher.

### How often does it update?

The server reads every feed every five minutes. ERCOT publishes in 15-minute intervals and Ameren publishes hourly day-ahead prices, so those change less often.

### My state isn't covered. Why?

Most of the Southeast is served by utilities that own their own generation and do not publish a public real-time price. The PJM states (Pennsylvania, New Jersey, Maryland, DC, Delaware, Virginia, Ohio, West Virginia) are waiting on a reliable public source. See [coverage](coverage.md#not-covered-yet). If you know of a feed for your area, [open an issue](../../../issues/new/choose).

### Can I use the API in my own app?

Yes. Please poll no more than every five minutes per provider and cache on your side. A link back to [gridprice.app](https://gridprice.app) is appreciated.

### How far back does the history go?

To July 22, 2026, for every feed. Ask for up to 400 days in one request.

### Is there an iPhone app?

Not yet. Android comes first, through Google Play; the App Store is next. [Join the beta](https://gridprice.app/#beta) to hear when it is ready.

### Can I see the source code?

No. GridPrice is a product I'm still building, so I'm showing what it does without giving the code away: the server and app source are private. This repository documents what it does and how it works, and the API is open for anyone to build on.

### Something looks wrong with a price.

Grid operators occasionally publish corrections, gaps or spikes. If a price looks off, [report it](../../../issues/new/choose) with the provider id and the time, and I will check it against the source.
