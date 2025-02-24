# Praktik-Sistem-Games
Tugas Movement Karakter

    using UnityEngine;
    public class PlayerController : MonoBehaviour
    {
    public float speed = 5.0f;
    public float jump = 9.0f;
    public Camera myCamera;
    
    // Batas pergerakan kamera
    public float minX = 2.77f; // Batas kiri
    public float maxX = 17.11f;  // Batas kanan
    public float minY = 0.02;  // Batas bawah
    public float maxY = 0.02f;   // Batas atas

    // Update is called once per frame
    void Update()
    {
        // Pergerakan player
        float x = Input.GetAxisRaw("Horizontal") * speed;
        float y = Input.GetAxisRaw("Vertical") * jump;
        transform.position += new Vector3(x, y, 0) * Time.deltaTime;

        // Posisi kamera mengikuti player
        FollowPlayer();
    }

    void FollowPlayer()
    {
        // Ambil posisi player
        Vector3 playerPosition = transform.position;

        // Batasi posisi kamera agar tidak keluar dari batas
        playerPosition.x = Mathf.Clamp(playerPosition.x, minX, maxX);
        playerPosition.y = Mathf.Clamp(playerPosition.y, minY, maxY);

        // Pertahankan posisi z kamera (jangan diubah)
        playerPosition.z = myCamera.transform.position.z;

        // Update posisi kamera
        myCamera.transform.position = playerPosition;
    }
}
