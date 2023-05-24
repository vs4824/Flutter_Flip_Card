# Flutter Flip Card

A component that provides a flip card animation. It could be used for hiding and showing details of a product.

## How to use

   ```
   import 'package:flip_card/flip_card.dart';
   ```

Create a flip card. The card will flip when touched

   ```
   FlipCard(
  fill: Fill.fillBack, // Fill the back side of the card to make in the same size as the front.
  direction: FlipDirection.HORIZONTAL, // default
  side: CardSide.FRONT, // The side to initially display.
  front: Container(
    child: Text('Front'),
  ),
  back: Container(
    child: Text('Back'),
  ),
);
   ```

You can also configure the card to only flip when desired by using a GlobalKey to toggle the cards (not recommended):

   ```
   GlobalKey<FlipCardState> cardKey = GlobalKey<FlipCardState>();

@override
Widget build(BuildContext context) {
  return FlipCard(
    key: cardKey,
    flipOnTouch: false,
    front: Container(
      child: RaisedButton(
        onPressed: () => cardKey.currentState.toggleCard(),
        child: Text('Toggle'),
      ),
    ),
    back: Container(
      child: Text('Back'),
    ),
  );
}
   ```

Recommended way to flip the card to avoid creating GlobalKeys:

   ```
   FlipCardController _controller;

@override
void initState() {
  super.initState();
  _controller = FlipCardController();
}

child: FlipCard(
  controller: _controller,
)

void doStuff() {
  // Flip the card a bit and back to indicate that it can be flipped (for example on page load)
  _controller.hint(
    duration: UIConfig.projectFlipHintDuration,
    total: UIConfig.projectFlipHintTotal,
  );

  // Tilt the card a bit (for example when hovering)
  _controller.hint(
    duration: UIConfig.projectFlipHintDuration,
    total: UIConfig.projectFlipHintTotal,
  );

  // Flip the card programmatically
  _controller.toggleCard();
}
   ```

You can auto-flip the widget after a certain delay without any external triggering.

   ```
   FlipCard(
  fill: Fill.fillBack, // Fill the back side of the card to make in the same size as the front.
  direction: FlipDirection.HORIZONTAL, // default
  side: CardSide.FRONT, // The side to initially display.
  front: Container(
    child: Text('Front'),
  ),
  back: Container(
    child: Text('Back'),
  ),
  autoFlipDuration: const Duration(seconds: 2), // The flip effect will work automatically after the 2 seconds
);
   ```