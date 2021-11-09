using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerScript2D : MonoBehaviour 
{
    private Rigidbody2D rd;
    private float HorizontalMove = 0f;
    private bool FacingRight = true;

    [Range(0, 15f)] public float jumpForce = 8f;


    public float speed = 1f;

    void Start()
    {
        rd = GetComponent<Rigidbody2D> ();
    }

    
    void Update()
    {
        if(Input.GetKeyDown(KeyCode.Space))
        {
            rd.AddForce(transform.up * jumpForce, ForceMode2D.Impulse);
        }
        
        HorizontalMove = Input.GetAxisRaw("Horizontal") * speed;

        if (HorizontalMove < 0 && FacingRight)
            {
            Flip();
        }
        else if (HorizontalMove > 0 && !FacingRight)
        {
            Flip();
        }


    } 

    private void FixedUpdate()
    {
        Vector2 targetVelocity = new Vector2(HorizontalMove * 10f, rd.velocity.y);
        rd.velocity = targetVelocity;
    }

    private void Flip()
    {
        FacingRight = !FacingRight;

        Vector3 theScale = transform.localScale;
        theScale.x *= -1;
        transform.localScale = theScale;
    }

}   

