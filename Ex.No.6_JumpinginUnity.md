# Ex.No: 6  Implementation of Jumping  behaviour- Unity
### DATE:    16/09/2025                                                                     
### REGISTER NUMBER : 212224230219
### AIM: 
To write a program to simulate the process of jumping in Unity.
### Algorithm:
```
1. Create a new 3D Unity project
2. Add a Plane
3. Right-click Hierarchy → 3D Object → Plane → Rename to Ground
4. Add a Cube (Player)
5. Right-click Hierarchy → 3D Object → Cube → Rename to Player
6. Set Position: (0, 0.5, 0)
7. Add a Rigidbody to the Player
8. With the Player selected: Inspector → Add Component → Rigidbody
9. Set Constraints > Freeze Rotation X, Z (optional for stability)
10.Create the Jump Script and Apply the Script Player
11.Run the game
Press Play
Press Spacebar to jump
Your cube should only jump when touching the ground
```
###
**Program **
```
using UnityEngine;

public class PlayerJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 5f;
    private bool isGrounded;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
            isGrounded = false;
        }
    }

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = true;
        }
    }
}
```
### Output:


<img width="1919" height="1025" alt="435607024-bfb72d21-f6dc-4935-ab48-4a978272d4cc" src="https://github.com/user-attachments/assets/40618f49-efbd-4e45-87d1-1033b168070a" />


<img width="1919" height="1021" alt="435607436-f8838d0d-e3b2-46c5-9a49-7a547e265924" src="https://github.com/user-attachments/assets/aa91344f-9e4e-4282-b973-9f2657606438" />





### Result:
Thus the simple jumping behavior was implemented successfully.
