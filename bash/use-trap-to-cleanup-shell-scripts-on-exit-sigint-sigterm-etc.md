# 2024-02-05 - TIL - Use Trap to Cleanup Shell Scripts on EXIT, SIGINT, SIGTERM, Etc.

Utilize `trap` to specify actions upon receiving signals like `EXIT`, `SIGINT`, `SIGTERM`.


## Usage

```sh
# This example performs the following:
#   1. Create a temporary file
#   2. Set up a trap to remove it when the script exits
#   3. Optionally, if an error occurs and you want to trigger cleanup manually, uncomment `trap cleanup ERR`

# Define a function to perform cleanup
cleanup() {
    echo "Performing cleanup..."
    # Remove the temporary file
    rm -f "$temp_file"
    echo "Cleanup done."
}

# Create a temporary file
temp_file=$(mktemp)

# Write something to the temporary file
echo "Temporary data" > "$temp_file"

# Set up the trap to call cleanup on script exit
trap cleanup EXIT

# Rest of the script logic goes here
# ...

# If an error occurs, you can manually trigger the cleanup
# trap cleanup ERR
```


## Use Cases

- Proper cleanup ensures that resources like temporary files, network connections, or locks are released promptly after they are no longer needed, freeing up system resources
- When a script is killed, it may leave forked processes behind. These can consume system resources and might cause problems if left unchecked
- Proper cleanup prevents data corruption by ensuring that temporary or partial data is removed before it's overwritten with new data
- Good cleanup practices can make scripts more robust by handling errors gracefully and providing meaningful feedback to users
- Well-structured cleanup code can make troubleshooting easier by providing clear indications of what went wrong and where
- Proper cleanup supports recovery by ensuring that the state of the system is consistent before the script starts executing, and clean after it finishes


## References

- [why is it important to cleanup shell scripts properly?](https://www.phind.com/search?cache=sh02jvyrys2um99zpn4xnojn)

