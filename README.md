# create-component-cli
Automatisez la création de composants React avec un script Bash

[**La video sur Youtube**](https://youtu.be/tMfx4Cb4IVk)


1. Créez un nouveau fichier appelé create-component.sh et ouvrez-le dans votre éditeur de texte préféré.
```bash
 touch create-component.sh
 ```

2. Ouvrez le fichier avec `open create-component.sh` et 
 ajoutez à ce fichier:
```bash
 #!/bin/bash

if [ $# -ne 2 ]; then
    echo "Usage: create-component <ComponentName> <path>"
    exit 1
fi

component_name="$1"
path="$2"

# Convert to PascalCase and camelCase
component_name_pascal="$(tr a-z A-Z <<<"${component_name:0:1}")${component_name:1}"
component_name_camel="$(tr A-Z a-z <<<"${component_name:0:1}")${component_name:1}"

# Create directory
component_dir="${path}/${component_name_pascal}"
mkdir -p "${component_dir}"

# Create ComponentName.tsx
tsx_file="${component_dir}/${component_name_pascal}.tsx"
cat > "${tsx_file}" <<- EOM
import styles from "./${component_name_camel}.module.scss"

type ${component_name_pascal}Props = {}

const ${component_name_pascal} = (props: ${component_name_pascal}Props) => {
    const {} = props
    return (<div className={styles.component}></div>)
}

export default ${component_name_pascal}
EOM

# Create componentName.module.scss
scss_file="${component_dir}/${component_name_camel}.module.scss"
cat > "${scss_file}" <<- EOM
.component {
}
EOM

echo "Component '${component_name_pascal}' created at '${component_dir}'"
```


3. Enregistrez le fichier et rendez-le exécutable:
```bash
chmod +x create-component.sh
```

4. Déplacez le script dans un répertoire de votre PATH, par exemple, /usr/local/bin, afin de pouvoir l'exécuter de n'importe où :
```bash
sudo mv create-component.sh /usr/local/bin/create-component
```

5. Maintenant, vous pouvez utiliser la commande create-component [componentName] [path] pour créer vos composants. Par exemple :
```bash
create-component BasedButton /path/to/components
```

6. Cela créera un répertoire BasedButton dans le chemin spécifié, ainsi que les fichiers BasedButton.tsx et basedButton.module.scss.

🎉

## Utilisation 

Vous aurez sans doute besoin de relancer votre terminal. 
Lorsque l'on veut créer un composant `Button` dans `src/components/[ici]` , il n'y a plus qu'à entrer la commande 
```bash
create-component Button ./src/components/
```
