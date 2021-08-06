# Breakout

This is a implementation of the game Breakout in Unity.

## Keypoints

* Unitys new Input System
* Create Blocks in Code
* Create a physic material and manipulate it so that it bounces off surfaces
* Lean how to use Unity
* Programming with C#


## Some Code examples
**Instantiate random blocks**
```c#
//Settings
public int rows = 5;
public int cols = 3;
public float width;
public float height;
public float xOffset = -5f;
public float yOffset = 3f;
private List<GameObject> activeBricks;

void Start()
    {
        activeBricks = new List<GameObject>();
        for(int row = 0; row < rows; row++)
        {
            for(int col = 0; col < cols; col++)
            {
                Brick newBrick = Instantiate<Brick>(brick, new Vector2(col*width+xOffset, row*height+yOffset), Quaternion.identity, bricks.transform);
                newBrick.HP = Random.Range(1, 4);
                activeBricks.Add(newBrick.gameObject);
            }
        }
    }
```
**Collisiondetection of the case: Ball hit a Brick**
```c#
void OnCollisionEnter2D(Collision2D col)
{
    if(col.gameObject.tag == "Ball")
    {
        BallToBrickCollision();
    }
}

void BallToBrickCollision()
{
    HP--;
    if(HP <= 0) {
        ActivateBrickFall();
    }
}
void ActivateBrickFall()
{
    coll.enabled = false;   //Dont interact with the ball or paddle => this is now just a visible effect and doesnt interact with the gameworld
    rb.gravityScale = 1;    //Let it fall!
    rb.constraints = RigidbodyConstraints2D.None; //To enable rotation while falling. Maybe for later improvements so that falling bricks can collide with each other.
}
```
Later the gamemanager will delete the falling brick if it isnt visible anymore.
