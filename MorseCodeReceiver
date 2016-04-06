/*
 * Morse Code receiver app information:
 *
 * Function: messageFinished(): stops the capturing process
 *
 *     You can call this function to let the app know that the 
 *     end-of-transmission signal has been received.
 *
 * -------------------------------------------------------
 *
 * ID: messageField: id of the message text area
 *
 *     This will be a textarea element where you can display
 *     the recieved message for the user.
 * 
 * -------------------------------------------------------
 *
 * ID: restartButton: id of the Restart button
 *
 *     This is a button element.  When clicked this should 
 *     cause your app to reset its state and begin recieving
 *     a new message.
 *
 */


// ADD YOUR ADDITIONAL FUNCTIONS AND GLOBAL VARIABLES HERE


/*
 * This function is called once per unit of time with camera image data.
 * 
 * Input : Image Data. An array of integers representing a sequence of pixels.
 *         Each pixel is representing by four consecutive integer values for 
 *         the 'red', 'green', 'blue' and 'alpha' values.  See the assignment
 *         instructions for more details.
 * Output: You should return a boolean denoting whether or not the image is 
 *         an 'on' (red) signal.
 */
var prevColour = "blue";
var redCounter = 0;
var blueCounter = 0;
var symbolToDecode = "";
var start = 1;
var lookupTable =
{
    ".-": "a",
    "-...": "b",
    "-.-.": "c",
    "-..": "d",
    ".": "e",
    "..-.": "f",
    "--.": "g",
    "....": "h",
    "..": "i",
    ".---": "j",
    "-.-": "k",
    ".-..": "l",
    "--": "m",
    "-.": "n",
    "---": "o",
    ".--.": "p",
    "--.-": "q",
    ".-.": "r",
    "...": "s",
    "-": "t",
    "..-": "u",
    "...-": "v",
    ".--": "w",
    "-..-": "x",
    "-.--": "y",
    "--..": "z",
    "-----": "0",
    ".----": "1",
    "..---": "2",
    "...--": "3",
    "....-": "4",
    ".....": "5",
    "-....": "6",
    "--...": "7",
    "---..": "8",
    "----.": "9",
    "-.--.": "(",
    "-.--.-": ")",
    ".-..-.": "\"",
    "........-..-": "$",
    "-..-.": "/",
    ".-.-.": "+",
    "---...": ":",
    ".-.-.-": ".",
    "--..--": ",",
    "..--..": "?",
    "-....-": "-",
    ".--.-.": "@",
    "-...-": "=",
    "..--.-..--.-": "_",
    "---.---.": "!",
    ".-.-": "<br／>",   //new line
    "...-.-": "messagefinished()"   //end of transmission
};



function decodeCameraImage(data)
{
    if (start == 1)
    {
        blueCounter = 0;
        start = 0;
    }


    var red = 0;
    var blue = 0;
    //gets the red and blue values of the image
    for (var i = 0; i < data.length; i += 4)
    {
        red += data[i];
        blue += data[i + 2];
    }


    //if the current image is red
    if (red > blue)
    {
        //if the previous image is red as well
        if (prevColour == "red")
        {
            redCounter++;
        }
        //if the previous image is not red
        else
        {
            if (blueCounter > 2 && blueCounter < 7)
            {
                for (var property in lookupTable)
                {
                    if (symbolToDecode == property)
                    {
                        document.getElementById('messageField').innerHTML += lookupTable[property];
                        prevColour = "red";
                        redCounter++;
                        blueCounter = 0;
                        symbolToDecode = "";
                        return true;
                    }
                }
            }
            else if (blueCounter > 6)
            {
                for (var property in lookupTable)
                {
                    if (symbolToDecode == property){
                        document.getElementById('messageField').innerHTML = document.getElementById('messageField').innerHTML + lookupTable[property] + " ";
                        prevColour = "red";
                        redCounter++;
                        blueCounter = 0;
                        symbolToDecode = "";
                        reture true;
                    }
                }
                //adds space to message text area
                document.getElementById('messageField').innerHTML += " ";
            }
            //increase red image counter and reset blue image counter, set previous image to red
            prevColour = "red";
            redCounter++;
            blueCounter = 0;
        }

        return true;
    }

    //if the current image is blue
    else
    {
        //if the previous image is blue as well
        if (prevColour == "blue")
        {
            blueCounter++;

        }
        //if the previous image is not blue
        else
        {
            if (redCounter == 1 || redCounter == 2)
            {
                symbolToDecode += ".";
            }
            else
            {
                symbolToDecode += "-";
            }

            redCounter = 0;
            blueCounter++;
            prevColour = "blue";
        }

        return false;
    }





    function reset()
    {
        redCounter = 0;
        blueCounter = 0;
        document.getElementById('messageField').innerHTML = "";
        symbolToDecode = "";
        start = 1;
        return;
    }

    document.getElementById('restartButton').onclick = reset;



}



