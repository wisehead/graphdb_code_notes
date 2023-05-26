#1.enum GraphObjectKey

```
#[derive(Clone, Serialize, Deserialize, Debug)]
pub enum GraphObjectKey {
    Vertex(VertexKey),
    Edge(EdgeKey),
}

```