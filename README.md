(FlappyBirdController.cs):

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class FlappyBirdController : MonoBehaviour
{
    public float jumpForce = 5f;
    private Rigidbody2D rb;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            rb.velocity = new Vector2(0, jumpForce);
        }
    }
}
```

Script de movimento do cenário (ScrollingBackground.cs):

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ScrollingBackground : MonoBehaviour
{
    public float scrollSpeed = 1f;
    private MeshRenderer meshRenderer;

    void Start()
    {
        meshRenderer = GetComponent<MeshRenderer>();
    }

    void Update()
    {
        float x = Mathf.Repeat(Time.time * scrollSpeed, 1);
        Vector2 offset = new Vector2(x, 0);
        meshRenderer.sharedMaterial.SetTextureOffset("_MainTex", offset);
    }
}

 (ObstacleSpawner.cs):

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ObstacleSpawner : MonoBehaviour
{
    public GameObject obstaclePrefab;
    public float spawnRate = 2f;
    public float spawnHeight = 3f;

    void Start()
    {
        StartCoroutine(SpawnObstacles());
    }

    IEnumerator SpawnObstacles()
    {
        while (true)
        {
            Instantiate(obstaclePrefab, new Vector3(transform.position.x, Random.Range(-spawnHeight, spawnHeight), 0), Quaternion.identity);
            yield return new WaitForSeconds(spawnRate);
        }
    }
}
```

 
