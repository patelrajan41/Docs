# Slot UI
## Slot Controls

#### Button Controls

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

#### Text Controls

Control | Description
:---: | ---
BetValue | Show current bet amount
LinesValue | Show current selected win lines
TotalBetValue | Show total bet amount (BetValue * Lines)
BalanceValue | Show current remaining balance
WinText | Visible if user recently won something

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

It holds [SlotData](#Slot-Data) and Game Property.

**Game Property** contains following properties :

&nbsp;&nbsp;&nbsp;&nbsp; Game Logo : Link of a logo image for currently loaded game

&nbsp;&nbsp;&nbsp;&nbsp; Game Name : Game name of currently loaded game

&nbsp;&nbsp;&nbsp;&nbsp; Version Name : Version name for the currently loaded game

&nbsp;&nbsp;&nbsp;&nbsp; Game ID : A unique id of a currently loaded game
