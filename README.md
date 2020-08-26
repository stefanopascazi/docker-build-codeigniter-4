### Usage

Create a .env and paste the correct environment value from CodeIgniter 4

Put .env file in root project directory

To run it:

    $ docker run -p 9090:80 -v $(pwd)/.env:/var/www/.env stedotdev/codeigniter-4

Using docker-compose to run it:

    version: '3.1'

    services:
    codeigniter:
        image: stedotdev/codeigniter-4
        restart: always
        container_name: codeigniter
        volumes: 
            - $(pwd)/.env:/var/www/.env

### How to create app/* project structure

Download sample app, public, writable, test from: [https://github.com/stefanopascazi/codeIgniter-4-sample-data-structure](https://github.com/stefanopascazi/codeIgniter-4-sample-data-structure)

Now you can use this set, and pass all your work into image via volumes or via Dockerfile.

Via docker-compose:

    version: '3.1'

    services:
    codeigniter:
        image: stedotdev/codeigniter-4
        restart: always
        container_name: codeigniter
        volumes: 
            - $(pwd)/.env:/var/www/.env
            - $(pwd)/app:/var/www/app
            - $(pwd)/public:/var/www/html
            - $(pwd)/writable:/var/www/writable
            - $(pwd)/test:/var/www/test

Via Dockerfile (preferer for production)

    FROM stedotdev/codeigniter-4

    # COPY all dependecies
    COPY ./web/app ./app
    COPY ./web/public ./html
    COPY ./web/writable ./writable

    # Setting correct USER:GROUP
    RUN chown -R www-data:www-data ./*