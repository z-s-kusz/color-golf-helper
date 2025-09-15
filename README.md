# About
This project helps visualize what colors can come out of a color generator that is given a max and min value for red, green and blue values. For use with [color-golf](https://color-golf.netlify.app/color-golf).

My color golf game is one of my projects I’m most proud of. It uses a very simple method to generate random colors in the RGB space. However since it is fully random it will sometimes generate very drab or washed out colors.

Initially I looked at using another color space that uses hue, saturation, and lightness values instead of red, green, and blue. That way I could force the saturation and lightness values into a space where no really terrible colors would pop up. But that created a problem that went against the whole point of the game. Who wants to just memorize the number code for orange? With RBG you feel like you’re mixing paints, you know how to make orange with a combo of mostly red and green with a splash of blue. You fail and try again, changing the values to try to get closer to the perfect shade, that's what makes it a game! HSL by definition doesn’t allow mixing colors, you tell it exactly what color to do then add the saturation and lightness.

Maybe one day I will pick colors in the HSL color space then convert them to RGB values but that didn’t sound as fun as making this :) .

## Developing
`npm i`

`npm run dev`
