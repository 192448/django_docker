FROM archlinux:latest as build

RUN pacman --noconfirm -Syu
RUN pacman --noconfirm -S python
RUN pacman --noconfirm -S python-pip

WORKDIR /usr/src/app

RUN python -m venv venv

RUN source venv/bin/activate

COPY requirements.txt .

RUN ./venv/bin/pip install -r requirements.txt

COPY . .

RUN ./venv/bin/python manage.py makemigrations
RUN ./venv/bin/python manage.py migrate

EXPOSE 8000

ENTRYPOINT ["./venv/bin/gunicorn", "app.wsgi"]
