# joe_docker example

Tiny example to accompany [joe_docker](https://github.com/keynmol/joe_docker). 

Let `IP_ADDRESS` be the host ip address - it will be your bridge IP address on Linux, or IP address of virtual machine on OS X/Windows (`docker-machine ip default`)

- Build containers:

    ```
    docker build -t jd_examples/summator summator/ && \
    docker build -t jd_examples/say_hello say_hello && \ 
    docker build -t jd_examples/say_comma say_comma && \ 
    docker build -t jd_examples/say_world say_world
    ```
- Run `joe_docker` and launch services immediately (note I'm using `docker-machine ip default` because I'm on OS X):

    ```
    joe_docker -c config.json --ip IP_ADDRESS | sh
    ```

Now go to `http://IP_ADDRESS:8080` and check that it says "Hello, world!".

It's produced by combining 4 Docker containers services with dependencies:

```sh
                               +--------------+
            +------------------+              |
            |                  |   say_comma  | - outputs ", "
            |                  |     :7701    |
  +---------v-----+            +--------------+
  |               |
  |   say_hello   | - outputs "Hello" + output from say_comma
  |     :7720     |
  +---------------+             +---------------+
               |                |               |
               |                |   say_world   | - outputs "world!"
               |                |    :7705      |
               |     +--------------------------+
               |     |
               |     |
         +-----v-----v----+
         |                |
         |    summator    | - sums outputs, printing "Hello, world!"
         |     :8080      |
         +----------------+


```