

loop - runs an infinte loop, no need to mention any conditions

```rust

fn main(){
    loop {
        //print Hi infinte times
        println!("Hi");
    }    
}

// give a break from inside of loop
fn main(){
    let mut _index: i32 = 0;

    let result : i32 = loop {
        _index += 1;
        println!("Index Value - {}",_index);
        if _index == 500 {            
            break _index 
        }        
    };

    println!("Result - {}",result);
}

```