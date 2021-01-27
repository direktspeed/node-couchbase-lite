```rust
// Open a database
let cfg = DatabaseConfiguration{directory: tmp_dir.path(), flags: CREATE};
let mut db = Database::open("rust_db, Some(cfg)).expect("opening db");

// Create a document
let mut doc = Document::new_with_id("foo");
let mut props = doc.mutable_properties();
props.at("greeting").put_string("Howdy!");
db.save_document(&mut doc, ConcurrencyControl::FailOnConflict).expect("saving");

// Read it back
let doc = db.get_document("foo").expect("reload document");
let props = doc.properties();
let greeting = props.get("greeting");
```
