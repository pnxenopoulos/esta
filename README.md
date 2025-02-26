# Esports Trajectories & Actions (ESTA)

[![Discord](https://img.shields.io/discord/868146581419999232?color=blue&label=Discord&logo=discord)](https://discord.gg/W34XjsSs2H) ![GitHub repo size](https://img.shields.io/github/repo-size/pnxenopoulos/esta) ![GitHub demo count](https://img.shields.io/badge/demos-1558-critical) [![awpy](https://img.shields.io/badge/made%20with-awpy-blueviolet)](https://github.com/pnxenopoulos/awpy) [![CC BY-SA 4.0](https://img.shields.io/badge/license-CC%20BY%20SA-lightgrey)](https://creativecommons.org/licenses/by-sa/4.0/) [![DOI](https://zenodo.org/badge/495219448.svg)](https://zenodo.org/badge/latestdoi/495219448)


Esports Trajectories and Actions (ESTA) is a large dataset of parsed Counter-Strike: Global Offensive (CSGO) demos which contains rich player action and location information. Each parsed demo:

- is a JSON compressed in `.xz` format, and is roughly 1-3 MB compressed/25-75 MB decompressed
- contains spatiotemporal data on player actions (damages, kills, grenade throws, bomb plants/defuses, flashes and weapon fires)
- contains frames ("game snapshots") parsed at 2 Hz, or 2 frames per in-game second
- is parsed using the [awpy](https://github.com/pnxenopoulos/awpy) parser
- is from a well-known tournament according to HLTV (all participants are known to the public. These are _not_ private demos)

The ESTA dataset is comprised of the "Online" (`data/online/`) and the "LAN" (`data/lan/`) subsets. "Online" contains 878 demos from top Online tournaments between January 2021 and May 2022. "Lan" contains 680 demos from top LAN tournaments between July 2021 and May 2022. The list of matches for each was compiled using [HLTV.org](https://www.hltv.org/). Visit HLTV to access a comprehensive list of tournaments and matches, along with their corresponding statistics and demos.

The ESTA data is non-exhaustive, and may lack some demos from the stated time frame or tournaments. For this reason, we do not recommend using ESTA to calculate player statistics (e.g., kills, ADR, etc.) for the time frame stated above. Instead, we recommend visiting HLTV to use their aggregation and statistics tools.
    
|  **Data** | **Demos** | **Rounds** | **Actions** | **Frames** | **Size** |
|:---------:|:---------:|:----------:|:-----------:|:----------:|:--------:|
|  _Online_ |    878    |   23,444   |     4.7m    |    4.4m    |   2.2G   |
|   _LAN_   |    680    |   18,338   |     3.9m    |    3.5m    |   1.7G   |
| **Total** |   1,558   |   41,782   |     8.6m    |    7.9m    |   3.9G   |  
    
ESTA has a variety of uses. For example, we use ESTA for win probability prediction, which we provide benchmarks for at the end of this README. ESTA may also prove useful for other prediction tasks such as trajectory prediction or unsupervised strategy identification. Outside of machine learning, ESTA may be useful for visualization, completing a class project or thesis, and for practicing data science.

## Usage
You can decompress a parsed demo by running 

```xz --decompress demo-to-open.xz```

> [!WARNING]
> ESTA data is only compatible with Awpy version 1.x -- current versions of Awpy 2.x and above are _not_ compatible!

You can install Awpy 1.3.1 (requires Golang >= 1.17) through pip by running 

```pip install awpy==1.3.1```

If you want to check out what a parsed demo looks like, we recommend using the GitHub web interface to locate an example `.xz`, rather than cloning the whole repository, which is a few GB.

## Example Data
Each parsed JSON contains demo metadata (such as the map, tick rate, what competition it is from, etc.), parser parameters used from awpy, the game server parameters, and a list of game rounds. In each game round, there exists round metadata (score, end reason, teams, etc.), along with six actions (kills, damages, bomb events, grenade throws, weapon fires and flashes), as well as a list of game frames, which are effectively game snapshots containing player information. We show an example of kill and frame output below.

#### Kill

```json
{
    "tick": 9582,
    "seconds": 25.71875,
    "clockTime": "01:30",
    "attackerSteamID": 76561198088580941,
    "attackerName": "febix",
    "attackerTeam": "",
    "attackerSide": "T",
    "attackerX": 509.1275939941406,
    "attackerY": 630.7955322265625,
    "attackerZ": 86.98412322998047,
    "attackerViewX": 327.601318359375,
    "attackerViewY": 1.9775390625,
    "victimSteamID": 76561198084596669,
    "victimName": "Rullaan Spotil KANDALFWOZ ;)",
    "victimTeam": "",
    "victimSide": "CT",
    "victimX": 781.4129638671875,
    "victimY": 491.81201171875,
    "victimZ": 87.30707550048828,
    "victimViewX": 153.6328125,
    "victimViewY": 1.0711669921875,
    "assisterSteamID": null,
    "assisterName": null,
    "assisterTeam": null,
    "assisterSide": null,
    "isSuicide": false,
    "isTeamkill": false,
    "isWallbang": false,
    "penetratedObjects": 0,
    "isFirstKill": true,
    "isHeadshot": true,
    "victimBlinded": false,
    "attackerBlinded": false,
    "flashThrowerSteamID": null,
    "flashThrowerName": null,
    "flashThrowerTeam": null,
    "flashThrowerSide": null,
    "noScope": false,
    "thruSmoke": false,
    "distance": 305.7054888578491,
    "isTrade": false,
    "playerTradedName": null,
    "playerTradedTeam": null,
    "playerTradedSteamID": null,
    "weapon": "Glock-18",
    "weaponClass": "Pistols"
}
```

#### Frame
```json
{
    "parseKillFrame": true,
    "tick": 8174,
    "seconds": 3.71875,
    "clockTime": "01:52",
    "t": {
        "side": "T",
        "teamName": "",
        "teamEqVal": 3550,
        "alivePlayers": 5,
        "totalUtility": 1,
        "players": [{
            "steamID": 76561198035759667,
            "name": "alo0o0o0o0",
            "team": "",
            "side": "T",
            "x": -1179.1435546875,
            "y": 483.21026611328125,
            "z": -55.96875,
            "velocityX": 109.83319854736328,
            "velocityY": 91.87308502197266,
            "velocityZ": 0,
            "viewX": 56.84326171875,
            "viewY": 3.33984375,
            "hp": 100,
            "armor": 0,
            "activeWeapon": "Knife",
            "totalUtility": 0,
            "isAlive": true,
            "isBlinded": false,
            "isAirborne": false,
            "isDucking": false,
            "isDuckingInProgress": false,
            "isUnDuckingInProgress": false,
            "isDefusing": false,
            "isPlanting": false,
            "isReloading": false,
            "isInBombZone": false,
            "isInBuyZone": false,
            "isStanding": true,
            "isScoped": false,
            "isWalking": false,
            "isUnknown": false,
            "inventory": [{
                "weaponName": "Glock-18",
                "weaponClass": "Pistols",
                "ammoInMagazine": 20,
                "ammoInReserve": 120
            }],
            "spotters": [],
            "equipmentValue": 200,
            "equipmentValueFreezetimeEnd": 200,
            "equipmentValueRoundStart": 200,
            "cash": 800,
            "cashSpendThisRound": 0,
            "cashSpendTotal": 0,
            "hasHelmet": false,
            "hasDefuse": false,
            "hasBomb": false,
            "ping": 32,
            "zoomLevel": 0
            }]
        },
        "ct": {},
        "world": [{
                "objectType": "bomb",
                "x": -1215.3546142578125,
                "y": 470.23406982421875,
                "z": -55.96875
        }],
        "bombPlanted": false,
        "bombsite": ""
}
```

## Benchmarks
We provide benchmarks for win probability prediction using the ESTA data. The benchmarks are available on [Google Colab](https://colab.research.google.com/drive/1Oqgr4LT3d9pCW4vj4isyR1AfNGtY50sF?usp=sharing). In the benchmarks, we compare gradient boosted trees (LightGBM, XGBoost) with set learning methods, like Deep Sets and Set Transformers.

We use the following hyperparameters:
- Default parameters provided by the corresponding packages for LightGBM and XGBoost.
- Default parameters for the MLP provided by the sklearn package. We use 0-1 scaling for the features.
- 10 early stopping rounds for all models.
- 100 epochs and a batch size of 32 for DeepSets and Set Transformers.
- Adam optimizer with a learning rate of 0.001.
- For DeepSets, we use one linear layer as the encoder and one linear layer for the decoder.
- For the Set Transformer, we use one ISAB layer (1 attention head, 16 induced points) as the encoder. For the decoder, we use a Pooling by Multihead Attention block (1 attention head), followed by a linear layer.

The hyperparameters are also available in the [Google Colab](https://colab.research.google.com/drive/1Oqgr4LT3d9pCW4vj4isyR1AfNGtY50sF?usp=sharing), particularly in the second to last block. To see the architecture parameters for DeepSets and Set Transformers, see the `DeepSet()` and `SetTransformer()` functions.
