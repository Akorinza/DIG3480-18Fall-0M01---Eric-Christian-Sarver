# DIG3480-18Fall-0M01---Eric-Christian-Sarver---Tutorial 1: Roll a Ball Tutorial
Eric Christian Sarver's GitHub repository for the class DIG3480-18Fall 0M01

Camera Controller

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraController : MonoBehaviour {

    public GameObject player;

    private Vector3 offset;

	// Use this for initialization
	void Start () {
        offset = transform.position - player.transform.position;
	}
	
	// Update is called once per frame
	void LateUpdate () {
        transform.position = player.transform.position + offset;
	}
}



Player Controller

using System.Collections;
using System.Collections.Generic;
using UnityEngine.UI;
using UnityEngine;

public class PlayerController : MonoBehaviour {

    public float speed;
    public Text countText;
    public Text winText;

    private Rigidbody rb;
    private int count;

    void Start ()
    {
        rb = GetComponent<Rigidbody>();
        count = 0;
        SetCountText();
        winText.text = "";
    }

    void FixedUpdate ()
    {
        float moveHorizontal = Input.GetAxis("Horizontal");
        float moveVertical = Input.GetAxis("Vertical");

        Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);

        rb.AddForce(movement * speed);

        if (Input.GetKey("escape"))
            Application.Quit();
    }

        void OnTriggerEnter(Collider other)
        {
        if (other.gameObject.CompareTag ("Pick Up"))
            {
                other.gameObject.SetActive (false);
                count = count + 1;
                SetCountText();
            }
        }
        void SetCountText ()
        {
        countText.text = "Count: " + count.ToString();
        if (count >= 12)
        {
            winText.text = "You Win!";
        }
        }

    }
    
    
    
Rotator
    
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Rotator : MonoBehaviour {


	// Update is called once per frame
	void Update () {
        transform.Rotate(new Vector3(15, 30, 45) * Time.deltaTime);
	}
}
