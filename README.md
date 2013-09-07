campuspartyeurope2013webgl
==========================

More info and accompanying slides can be found here: http://blog.softwareispoetry.com/2013/09/campus-party-europe-getting-into-3d-and.html

To run the code, you'll need to serve the files from a server.

In the talk I was serving the files from a xampp installation of Apache.
http://www.apachefriends.org/en/xampp.html

You can find the full set of tutorials at the learningwebgl.com website.

The lesson we covered was lesson6

lesson6a
--------
Rather than rotate the cube, we use yRot to make the cube go up and down.

mat4.translate(mvMatrix, [xRot, yRot, z]);

//mat4.rotate(mvMatrix, degToRad(xRot), [1, 0, 0]);
//mat4.rotate(mvMatrix, degToRad(yRot), [0, 1, 0]);



lesson6b
--------
We move the cube back in the negative z plane, and restrict it's movement to the edges of the screen.
var speedDelta = 1000.0;

if( yPos > 20 )
{
    if( ySpeed < 0 )
    {
        yPos += (ySpeed * elapsed) / speedDelta;
    }
}
else if( yPos < -20 )
{
    if( ySpeed > 0 )
    {
        yPos += (ySpeed * elapsed) / speedDelta;
    }
}
else
{
    yPos += (ySpeed * elapsed) / speedDelta;
}

if( xPos > 20 )
{
    if( xSpeed < 0 )
    {
        xPos += (xSpeed * elapsed) / speedDelta;
    }
}
else if( xPos < -20 )
{
    if( xSpeed > 0 )
    {
        xPos += (xSpeed * elapsed) / speedDelta;
    }
}
else
{
    xPos += (xSpeed * elapsed) / speedDelta;
}



lesson 6c
---------
Here we attempted to draw multiple cubes by creating a Player class and putting xPos and yPos variables inside.

for( var i=0; i<players.length; ++i )
{
	drawPlayer( player[i] );
}

Note: I've left two lines of code in the drawPlayer function commented out. If you comment them in, you'll see how the push/pop matrix stack operations affect the drawing states.



lesson 6d
---------
Some collision code is introduced to block intersections.

function canMove(player)
{
	var playerSize = 1.5;
	var minX = player.xPos - playerSize;
	var maxX = player.xPos + playerSize;
	var minY = player.yPos - playerSize;
	var maxY = player.yPos + playerSize;

	for( var i=0; i<players.length; ++i )
	{
	    var opponent = players[i];
	    if( player !== opponent )
	    {
	        var oppMinX = opponent.xPos - playerSize;
	        var oppMaxX = opponent.xPos + playerSize;
	        var oppMinY = opponent.yPos - playerSize;
	        var oppMaxY = opponent.yPos + playerSize;

	        if( maxX >= oppMinX && minX <= oppMaxX )
	        {
	            if( maxY >= oppMinY && minY <= oppMaxY )
	            {
	                return false;
	            }
	        }
	    }
	}
	return true;
}

BONUS: See if you can improve on the code to allow for movement away after a collision is made.