// PlayerController.cs
using UnityEngine;

[RequireComponent(typeof(CharacterController))]
public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 720f; // degrees per second
    CharacterController cc;
    Vector3 input;

    void Start()
    {
        cc = GetComponent<CharacterController>();
    }

    void Update()
    {
        // basic WASD / joystick movement
        input = new Vector3(Input.GetAxis("Horizontal"), 0f, Input.GetAxis("Vertical"));
        if (input.magnitude > 0.01f)
        {
            Vector3 move = transform.TransformDirection(input.normalized) * moveSpeed * Time.deltaTime;
            cc.Move(move);

            // rotate towards move dir
            Quaternion target = Quaternion.LookRotation(input);
            transform.rotation = Quaternion.RotateTowards(transform.rotation, target, rotateSpeed * Time.deltaTime);
        }

        if (Input.GetMouseButtonDown(0))
        {
            // basic attack
            TryAttack();
        }
        if (Input.GetKeyDown(KeyCode.Q))
        {
            // cast skill 1
            CastSkill1();
        }
    }

    void TryAttack()
    {
        // trigger attack animation and raycast for hit detection (simple)
        Debug.Log("Attack!");
    }

    void CastSkill1()
    {
        Debug.Log("Cast Skill 1");
        // spawn projectile or AoE effect
    }
}

