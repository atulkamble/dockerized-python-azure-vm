```
cd Downloads
chmod 400 key.pem
ssh -i key.pem azureuser@4.240.104.149

sudo apt update -y
sudo apt list --upgradable
sudo apt upgrade -y

sudo -i passwd

sudo apt install python3 -y
sudo apt install python-is-python3
python --version

sudo apt install python3-pip -y
pip install flask
sudo apt install python3-flask
pip3 show flask

pip install --upgrade pip

sudo apt install git -y
git --version

sudo apt install docker.io -y
sudo usermod -aG docker $USER

sudo systemctl start docker
sudo systemctl enable docker

sudo docker login

sudo mkdir project
cd project

sudo touch app.py
sudo nano app.py

sudo touch requirements.txt
sudo nano requirements.txt

python app.py

sudo touch Dockerfile

sudo docker build  -t flask-app .

sudo docker build  -t atuljkamble/flask-app .

sudo docker images

sudo docker run -p 5000:5000 -it atuljkamble/flask-app

sudo docker push atuljkamble/flask-app


```


