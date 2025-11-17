# Ex.No: 10  Implementation of 2D/3D game - Escape from the Falling Object Game
### DATE:  10/11/2025                                                                          
### REGISTER NUMBER : 212224230219
### AIM: 
To develop a Escape from the Falling Object Game in Unity
### Algorithm:
```
1. Create a new Unity project.
2. Add a Player GameObject to the scene.
3. Add a FallingObject GameObject to the scene.
4. Attach the PlayerController script to the Player GameObject.
5. Attach the FallingObject script to the FallingObject GameObject.
6. Set the Player GameObject's tag and add a Collider2D (if needed).
7. Set the Ground GameObject with tag "Ground" and add a Collider2D with IsTrigger enabled.
8. In the PlayerController script, read horizontal input and move the player each frame (in Update).
9. In the FallingObject script, move the object downwards each frame and check for collision with the ground using OnTriggerEnter2D.
10. If the falling object collides with the ground, destroy the player object.
```  
### Program:
# Bullet.cs
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Bullet : MonoBehaviour {

	public float speed = 20f;
	public int damage = 40;
	public Rigidbody2D rb;
	public GameObject impactEffect;

	// Use this for initialization
	void Start () {
		rb.velocity = transform.right * speed;
	}

	void OnTriggerEnter2D (Collider2D hitInfo)
	{
		Enemy enemy = hitInfo.GetComponent<Enemy>();
		if (enemy != null)
		{
			enemy.TakeDamage(damage);
		}

		Instantiate(impactEffect, transform.position, transform.rotation);

		Destroy(gameObject);
	}
	
}

```

# CharacterController2D.cs
```

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Bullet : MonoBehaviour {

	public float speed = 20f;
	public int damage = 40;
	public Rigidbody2D rb;
	public GameObject impactEffect;

	// Use this for initialization
	void Start () {
		rb.velocity = transform.right * speed;
	}

	void OnTriggerEnter2D (Collider2D hitInfo)
	{
		Enemy enemy = hitInfo.GetComponent<Enemy>();
		if (enemy != null)
		{
			enemy.TakeDamage(damage);
		}

		Instantiate(impactEffect, transform.position, transform.rotation);

		Destroy(gameObject);
	}
	
}


```

# Enemy.cs
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Enemy : MonoBehaviour {

	public int health = 100;

	public GameObject deathEffect;

	public void TakeDamage (int damage)
	{
		health -= damage;

		if (health <= 0)
		{
			Die();
		}
	}

	void Die ()
	{
		Instantiate(deathEffect, transform.position, Quaternion.identity);
		Destroy(gameObject);
	}

}

```

# PlayerMovement.cs
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMovement : MonoBehaviour {

	public CharacterController2D controller;
	public Animator animator;

	public float runSpeed = 40f;

	float horizontalMove = 0f;
	bool jump = false;
	bool crouch = false;

	// Update is called once per frame
	void Update () {

		horizontalMove = Input.GetAxisRaw("Horizontal") * runSpeed;

		animator.SetFloat("Speed", Mathf.Abs(horizontalMove));

		if (Input.GetButtonDown("Jump"))
		{
			jump = true;
			animator.SetBool("IsJumping", true);
		}

		if (Input.GetButtonDown("Crouch"))
		{
			crouch = true;
		} else if (Input.GetButtonUp("Crouch"))
		{
			crouch = false;
		}

	}

	public void OnLanding ()
	{
		animator.SetBool("IsJumping", false);
	}

	public void OnCrouching (bool isCrouching)
	{
		animator.SetBool("IsCrouching", isCrouching);
	}

	void FixedUpdate ()
	{
		// Move our character
		controller.Move(horizontalMove * Time.fixedDeltaTime, crouch, jump);
		jump = false;
	}
}
```

# PrefabWeapon.cs
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PrefabWeapon : MonoBehaviour {

	public Transform firePoint;
	public GameObject bulletPrefab;
	
	// Update is called once per frame
	void Update () {
		if (Input.GetButtonDown("Fire1"))
		{
			Shoot();
		}
	}

	void Shoot ()
	{
		Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
	}
}

```

# RayCastWeapon.cs

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class RayCastWeapon : MonoBehaviour {

	public Transform firePoint;
	public int damage = 40;
	public GameObject impactEffect;
	public LineRenderer lineRenderer;
	
	// Update is called once per frame
	void Update () {
		if (Input.GetButtonDown("Fire1"))
		{
			StartCoroutine(Shoot());
		}
	}

	IEnumerator Shoot ()
	{
		RaycastHit2D hitInfo = Physics2D.Raycast(firePoint.position, firePoint.right);

		if (hitInfo)
		{
			Enemy enemy = hitInfo.transform.GetComponent<Enemy>();
			if (enemy != null)
			{
				enemy.TakeDamage(damage);
			}

			Instantiate(impactEffect, hitInfo.point, Quaternion.identity);

			lineRenderer.SetPosition(0, firePoint.position);
			lineRenderer.SetPosition(1, hitInfo.point);
		} else
		{
			lineRenderer.SetPosition(0, firePoint.position);
			lineRenderer.SetPosition(1, firePoint.position + firePoint.right * 100);
		}

		lineRenderer.enabled = true;

		yield return 0;

		lineRenderer.enabled = false;
	}
}

```


### Output:

![WhatsApp Image 2025-11-11 at 14 22 32_5ac4e790](https://github.com/user-attachments/assets/404cfac2-bdcc-43b7-b5f7-53a3f0d36903)


![WhatsApp Image 2025-11-11 at 14 23 18_ab9706ff](https://github.com/user-attachments/assets/14940da4-3349-4621-adec-d5393157a3f3)


### Result:
Thus the game Escape from the Falling Object Game was developed using Unity.
