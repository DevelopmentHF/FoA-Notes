# Working With Files in C

## Default files

When executing a C program, **3** files become immediately available to use. <br>
- stdin
- stout
- stderr

>Note: printf() is just a call to `fprintf(stdout, )`<br>
>To write to any file, just `fprintf(yourfile, ...)`; <br>
>This applies to scanf as well. <br>

Error messages are written through a call to fprintf specifying **stderr** as the output file. <br>

<br>

---

<br>

## Opening files

```c
FILE*
fopen(const char* filename, const char* mode);
```

Different access modes include `"r" = read`, `"w" = write`, `"a" = append`. <br>

>Note: A "+" operator can be used in the access argument to provide dual functionality. <br>

"w+" allows for **writing** and **reading**.<br>
"r+" allows for **reading** and **appending**. Unlike the others, this mode does not create a new file if it doesn't already exist<br>
"a+" allows for **appending** and **reading**.<br>

<br>

---

<br>

## Writing to files 

Used to write data from an **array** into a file. <br>
This will overwrite any existing content. <br>

```c
size_t
fwrite(const void* ptr, size_t size, size_t nelem, FILE* fp);
```

Returns the number of elements written to the file from the array `ptr`, assert that this is correct after completing the operation. <Br>

<br>

---

<br>

## Reading from files

If a file has been opened in `"w"` access mode, first use `freopen()` to change access mode. <br>
This will read `nelems` into an array with each element being of the same size. <br>

```c
size_t
fread(void* ptr, size_t size, size_t nelem, FILE* fp);
```

Returns the number of values successfully read into the array `ptr`. <br>

<br>

---

<br>

## Closing files

After finishing operating on a file, you ***must*** close it to flush all buffers. <br>

```c
int
fclose(FILE* fp);
```

Returns `0` on success or `EOF` on failure. <br>
<br>

---

<br>

## Other

>***IMPORTANT***: After **each** file operation, make sure to check for failures through assertions. <br>
>For example, after assigning a file pointer through fopen(), assert that fp != NULL. <br>

Read a line from a fle and store in a string: <br>
```c
char*
fgets(char* str, int n, FILE* fp);
```
