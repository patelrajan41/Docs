

# snb-unity-client
This is a repository for the slot unity client - Android & iOS.  

# Unity Slot Demo
This repository provides slot integration in unity engine.

## Plug-In
This  project consist of  
* [Asset bundle browser](https://assetstore.unity.com/packages/tools/utilities/asset-bundle-browser-93571)
* [Odin inspector](https://assetstore.unity.com/packages/tools/utilities/odin-inspector-and-serializer-89041)
* [Json.net](https://assetstore.unity.com/packages/tools/input-management/json-net-for-unity-11)

There are several steps that needs to be take care of:
* [View Setup](#view-setup)

* [Service Manager](#service-manager)

* [Slot Data](#slot-data)

* [Slot Machine UI](#slot-machine-ui)

* [Asset Bundle](#asset-bundle)

##  View Setup
View Controller is responsible for handling all views.

-- Image Here --

GameLoad event Occurs in ViewWelcome Script
It will show all available games from webserver. This views are available in `ViewWelcome -> UICanvas -> ViewContent-> SlotSelectionScrollView -> Viewport -> Content`.

## Service Manager

All Web API are handled in ServiceManager singleton script. It is responsible to  populate all game data into the game.

**LoadGameList** : Loads all available list of games into the game.

   **Load SlotSymbols** : Loads all symbols from specified slot game.

**Load GameData** : Loads all initial game data from specified slot game.

**Load  Paytable** : Loads all paytable data and store into payout hashtable.

**Increase BetLine** : Request to Increase BetLine

**Decrease BetLine** : Request to Dcrease BetLine

**Increase Bet Amount** : Request to Increase Bet Amount

**Decrease Bet Amount** : Request to Decrease Bet Amount

**Max Bet** : Request to create Max Bet

Service Manager Script contains following properties :

**Link** : URL for API

**Create Slot with Asset Bundle** : It is boolean value. If true then Asset Bundle will be downloaded from URL else it will load from local asset bundle.

## Slot Data

*Show current configuration of Slot in Unity Inspector. It includes following data:*

**Slot Symbol Dictionary** : Contains all the slot symbols that were used in current game

**Initial Reel Dictionary** : Symbols that will be shown to user when reels stops.

**Spin Slot Reel Dictionary** : Symbols in specific reel. It size may differ for each reel.

**Player Statistics** : 

&nbsp;&nbsp;&nbsp;&nbsp; Line : Show current selected win lines

&nbsp;&nbsp;&nbsp;&nbsp; Bet : show current bet amount

&nbsp;&nbsp;&nbsp;&nbsp; Total Bet : Show total bet amount (BetValue * Lines)

&nbsp;&nbsp;&nbsp;&nbsp; Balance : Show current remaining balance

**Paylines** : It contains data for all paylines in binary format. Ex. 010 010 010 010 010. Column is specified by space in following example.

**Payout** : It is calculated by *Mutliplying CurrentBetAmount with `* of Kind` win's multiplier.*

## Game Manager

It holds [SlotData](#slot-data) and Game Property.

**Game Property** contains following properties :

&nbsp;&nbsp;&nbsp;&nbsp; **Game Logo** : Link of a logo image for currently loaded game

&nbsp;&nbsp;&nbsp;&nbsp; **Game Name** : Game name of currently loaded game

&nbsp;&nbsp;&nbsp;&nbsp; **Version Name** : Version name for the currently loaded game

&nbsp;&nbsp;&nbsp;&nbsp; **Game ID** : A unique id of a currently loaded game

## Slot Machine UI

### Winnnings UI

Shows particles around winning symbol and shows winning lines on slot win and free spin expand win.

It has some events listed below:

**AnimateWinLine** : It consist of each win line. Used to show win line one by one or all at once.

**AnimateSymbolInLine** : Used to animate symbol when it is the part of winning combination.

**ResetAnimatingSymbol** : Clears UI when no need to animate Winnings UI.

### Paytable Popup 

As per design slot info, It  may have different interaction with UI (i.e. sliders, tab, popups, etcetra)

UIScript should be created to interact with these kind of UI.

* The script must have following name space. `Games.CasinoSlot.slotName`
* Must override UIPopupMenu script
* All the UI event must be handle by this script.

### Slot Controls

##### Button Controls

Control | Description| Method to Call
:---: | --- | :---:
Spin | Start Spin | SlotUI.SpinButtonTapped
Auto | Spin Automatically until user stops it | SlotUI.AutoButtonTapped
Turbo | All reels rotate at once | SlotUI.TurboButtonTapped
MaxBet | Set current bet value to maximum from predefined array of values | SlotUI.MaxBetButtonTapped
Bet - Increase | Increase bet value from predefined array of values | SlotUI.IncreaseBetAmountButtonTapped
Bet - Decrease | Decrease bet value from predefined array of values | SlotUI.DecreaseBetAmountButtonTapped
Lines - Increase | Increase win lines | SlotUI.IncreaseBetLineButtonTapped
Lines - Decrease | Decrease win lines | SlotUI.DecreaseBetLineButtonTapped
Navigate to Paytable | Show all the information regarding Paytable | SlotUI.PayoutButtonClicked

##### Text Controls

Control | Description
:---: | ---
BetValue | Show current bet amount
LinesValue | Show current selected win lines
TotalBetValue | Show total bet amount (BetValue * Lines)
BalanceValue | Show current remaining balance
WinText | Visible if user recently won something

## Asset Bundle

### Asset Bundle Manager

It holds all the details regarding asset bundle.

**Standalone URL** : It is the link of Assest Bundle for PC (Windows, Linux, Mac)

**Android URL** : It is the link of Assest Bundle for all Android devices including tablets, samrtphones.

**iOS URL** : It is the link of Assest Bundle for all iOS devices including iPads, iPhone.

**Asset URL** : Target platform url will be assigned to this variable

**Asset Bundle** : Currently loaded asset bundle

### How to create Asset Bundle?

Nowadays, Asset Bundle's are created using **Asset Bundle Browser** in Unity3D. It is the easiest way.

1. Create new Asset Bundle from Asset Bundle Browser. For this Right Click in Asset Bundle Browser and Press **Add New Bundle**. Name it something. Ex. SampleSlotGame
2. Select **SlotMachine** Prefab and all slot Symbol's Prefabs from Project Panel.
> To ensure what will be included in asset bundle before creating it, Right Click on selected prefabs and click **Select Dependencies**. It will show all the files selected which will be included in asset bundle.
3. Switch to Asset Bundle Browser's *Configure* tab.
4. Drag and Drop all selected prefabs into Asset Bundle Browser.
5. Switch your tab from Configure to Build.
6. Select your **Build Target**.
7. Enter your output path. You can either copy and paste path or Browse it.
8. Set **Compression** method to *Standard Compression (LZMA)*.
9. Click on Build. On successful build, it will store newly created asset bundle to your output path.

### How to create slot Symbol animation prefab?

1. Add new game object `Image` into Hierarchy. Set it's width and height according to symbol image resolution.
2. Rename it to Symbol ID from API response. To do so you can also get ID of Symbol from SlotData.
3. You need to create two animation clip for it.
   - `SymbolDefault`
   - `Symbol`
> To create animation clip, Select animation panel and press Create while GameObject is selected.
4. Drag symbol image into `Source Image` in `Inspector` under `Image` Component.
5. Now switch to Animation Panel and select `SymbolDefault` clip.
6. Drag first sprite of sprite sheet into animation view.
7. Now select `Symbol` clip. Add all sprites into it and adjust your animation like duration, samples, etc.
8. Now open Animation Panel. `SymbolDefault` clip already added. Add `Symbol` clip into view.
9. Add `Bool` parameter. Rename it as `IsAnimated`. Uncheck it if it is already checked.
10. Right click on `SymbolDefault` and `Make Transition` to `Symbol`. Do in reverse order to. `Symbol` to `SymbolDefault`.
11. Select transition `SymbolDefault` to `Symbol`. Uncheck `Has Exit Time` parameter from inspector. Add condition `IsAnimated`. Set it to true.
> You can add condition by clicking plus button under `Conditions` in Inspector.
12. Select transition `Symbol` to `SymbolDefault`. Uncheck `Has Exit Time` parameter from inspector. Add condition `IsAnimated`. Set it to false.
13. Drag `GameObject` from `Hierarchy` to `Project`. Now your symbol prefab is ready to use. You can create all other symbol's prefab following this steps.
