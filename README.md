# Bad Room Codes
**WARNING: The file `bad_codes.json` contains some offensive stuff, so read through at your own discretion!**
## Background
The video game we are developing, [Sneaksters](https://www.reddit.com/r/Sneaksters), is made to be played in local groups, not necessarily with people on the other side of the globe. We took inspiration from the Jackbox Party Pack games, which generate a four-letter code that players use to join a room.
However, there is a problem - when you're using random combinations of letters, it's [very possible to end up with very inappropriate strings](https://jackboxgames.com/2014/11/11/room-censored-codes/). Jackbox explains in a blog post that they set up a list of "illegal" codes in their games that prevent anything inappropriate from getting through.
We looked around on the internet for an open-source version, but couldn't find anything, so we decided to make one ourselves. In the interest of lightening the burden for fellow developers, we're making our list open-source so that anyone can use or contribute to it.
## Useage
The list is contained in `bad_codes.json`, under the name `"codes"`. You can access it just as you would any other JSON array.

A simple example using Python:
```python
import json
code = input("Enter a code: ")
with open("bad_codes.json", "r") as f:
	jsonFile = json.loads(f.read())
	if code in jsonFile["codes"]:
		print("This code is bad!")
	else:
		print("This code is good")
```


An example using Unity and C#:
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System.Linq;

public class BadCodeParser : MonoBehaviour {
	string code; // declare the value of this string first!
	
	void Start() {
		string badCodesJson = System.IO.ReadAllLines("bad_codes.json");
		BadCodes badCodesObject = JsonUtility.FromJson<BadCodes>(badCodesJson);
		if (badCodesObject.codes.Contains(code) {
			Debug.Log("This code is bad!");
		} else {
			Debug.Log("This code is good");
		}
		
	}
}

[Serializeable]
public class BadCodes {
	public string about;
	public string credit;
	public string warning;
	public string[] codes;
}
```