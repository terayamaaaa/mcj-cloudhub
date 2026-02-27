stack = ${1:-mcj-cloudhub}
envfile = ./.env

include $(envfile)
export


devsetup:
		mkdir -p mcj-data && sudo bash localsetup.sh
devup:
		docker compose -f docker-compose.yml --env-file $(envfile) --profile moodle up -d
devdown:
		docker compose -f docker-compose.yml --env-file $(envfile) down
devdestroy:
		docker compose -f docker-compose.yml --env-file $(envfile) down -v
devrestart:
		docker compose -f docker-compose.yml --env-file $(envfile) down && \
		docker compose -f docker-compose.yml --env-file $(envfile) --profile moodle up -d

build:
		docker compose -f docker-compose.yml --env-file $(envfile) build
up:
		docker stack deploy -c docker-stack.yml $(stack)
down:
		docker stack rm $(stack)
config:
		docker compose -f docker-stack.yml config