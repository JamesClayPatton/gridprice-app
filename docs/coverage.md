# Coverage

47 price feeds across 33 states, from nine sources.

## By feed

| Source | Provider id | Area | Interval |
|---|---|---|---|
| **ComEd** | `comed` | Northern Illinois, ComEd Hourly Pricing | 5 minutes, live |
| **Ameren Illinois** | `ameren-il` | Central and southern Illinois, Power Smart Pricing | 1 hour, day-ahead |
| **ERCOT** | `ercot-lz_houston` | Houston (CenterPoint) | 15 minutes, live |
| | `ercot-lz_north` | Dallas–Fort Worth and North Texas (Oncor) | 15 minutes, live |
| | `ercot-lz_south` | South Texas | 15 minutes, live |
| | `ercot-lz_west` | West Texas | 15 minutes, live |
| | `ercot-lz_aen` | Austin Energy | 15 minutes, live |
| | `ercot-lz_cps` | San Antonio, CPS Energy | 15 minutes, live |
| **NYISO** | `nyiso-nyc` | New York City | 5 minutes, live |
| | `nyiso-longil` | Long Island | 5 minutes, live |
| | `nyiso-hudvl` | Hudson Valley | 5 minutes, live |
| | `nyiso-capitl` | Capital region, Albany | 5 minutes, live |
| | `nyiso-centrl` | Central New York | 5 minutes, live |
| | `nyiso-west` | Western New York, Buffalo | 5 minutes, live |
| **ISO New England** | `isone-ma` | Massachusetts | 5 minutes, live |
| | `isone-ct` | Connecticut | 5 minutes, live |
| | `isone-ri` | Rhode Island | 5 minutes, live |
| | `isone-nh` | New Hampshire | 5 minutes, live |
| | `isone-vt` | Vermont | 5 minutes, live |
| | `isone-me` | Maine | 5 minutes, live |
| **MISO** | `miso-mn` | Minnesota | 5 minutes, live |
| | `miso-wi` | Wisconsin | 5 minutes, live |
| | `miso-ia` | Iowa | 5 minutes, live |
| | `miso-mi` | Michigan | 5 minutes, live |
| | `miso-in` | Indiana | 5 minutes, live |
| | `miso-mo` | Missouri | 5 minutes, live |
| | `miso-ar` | Arkansas | 5 minutes, live |
| | `miso-la` | Louisiana | 5 minutes, live |
| | `miso-ms` | Mississippi | 5 minutes, live |
| **SPP** | `spp-ok` | Oklahoma | 5 minutes, live |
| | `spp-ks` | Kansas | 5 minutes, live |
| | `spp-ne` | Nebraska | 5 minutes, live |
| | `spp-sd` | South Dakota | 5 minutes, live |
| | `spp-nd` | North Dakota | 5 minutes, live |
| **CAISO** | `caiso-np15` | Northern California | 5 minutes, live |
| | `caiso-sp15` | Southern California | 5 minutes, live |
| **Western EIM** | `eim-pge` | Portland General Electric (Oregon) | 5 minutes, live |
| | `eim-pacw` | PacifiCorp West (Oregon, Washington, Northern California) | 5 minutes, live |
| | `eim-psei` | Puget Sound Energy (Washington) | 5 minutes, live |
| | `eim-nevp` | NV Energy (Nevada) | 5 minutes, live |
| | `eim-azps` | Arizona Public Service | 5 minutes, live |
| | `eim-ipco` | Idaho Power | 5 minutes, live |
| | `eim-pace` | PacifiCorp East | 5 minutes, live |
| | `eim-pace-ut` | PacifiCorp East, Utah | 5 minutes, live |
| | `eim-pace-wy` | PacifiCorp East, Wyoming | 5 minutes, live |
| | `eim-nwmt` | NorthWestern Energy (Montana) | 5 minutes, live |
| | `eim-pnm` | PNM (New Mexico) | 5 minutes, live |

## By state

The map on [gridprice.app](https://gridprice.app) lights up each state with one representative feed:

| State | Feed | State | Feed |
|---|---|---|---|
| Arizona | `eim-azps` | Missouri | `miso-mo` |
| Arkansas | `miso-ar` | Montana | `eim-nwmt` |
| California | `caiso-sp15` | Nebraska | `spp-ne` |
| Connecticut | `isone-ct` | Nevada | `eim-nevp` |
| Idaho | `eim-ipco` | New Hampshire | `isone-nh` |
| Illinois | `comed` | New Mexico | `eim-pnm` |
| Indiana | `miso-in` | New York | `nyiso-nyc` |
| Iowa | `miso-ia` | North Dakota | `spp-nd` |
| Kansas | `spp-ks` | Oklahoma | `spp-ok` |
| Louisiana | `miso-la` | Oregon | `eim-pge` |
| Maine | `isone-me` | Rhode Island | `isone-ri` |
| Massachusetts | `isone-ma` | South Dakota | `spp-sd` |
| Michigan | `miso-mi` | Texas | `ercot-lz_north` |
| Minnesota | `miso-mn` | Utah | `eim-pace-ut` |
| Mississippi | `miso-ms` | Vermont | `isone-vt` |
| | | Washington | `eim-psei` |
| | | Wisconsin | `miso-wi` |
| | | Wyoming | `eim-pace-wy` |

## What these prices are

ComEd and Ameren publish the hourly supply rate their hourly-pricing customers actually pay. Everywhere else, the price is the grid operator's real-time wholesale price for that zone, converted from dollars per MWh to cents per kWh.

Your bill adds delivery charges, taxes and fees on top, and those do not change by the hour. So the GridPrice number is not your all-in rate, but it is the part that tells you **when** power is cheap or expensive. If your plan follows wholesale prices (common in Texas, and the whole point of ComEd and Ameren hourly pricing), it moves your bill directly.

## Not covered yet

- **PJM** (Pennsylvania, New Jersey, Maryland, DC, Delaware, Virginia, Ohio, West Virginia): the feeds are wired up but not shown, pending a reliable public source.
- **The Southeast** (Georgia, the Carolinas, Florida, Alabama, Tennessee): mostly vertically integrated utilities with no public real-time price.

Want a utility or zone added? [Open an issue](../../../issues/new/choose).
