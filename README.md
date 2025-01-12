# React и MF
### Пример проекта микрофронтенда 
- React
- Webpack Module Federation

### Создание микрофронтенда
```bash
npx create-mf-app
npm install
npm start
```

### webpack.config.js
```js
export default function UsersTestControl() {
    return <div>Это тестовый компонент из проекта Users</div>
}

// в микрофронтенде
exposes: {
    './UsersTestControl': './src/components/UsersTestControl.js',
}, 

// в host или другом микрофронтенде
remotes: {
    'users': 'users@http://localhost:8081/remoteEntry.js',
}, 

// ленивый import
const UsersTestControl = lazy(() => import('users/UsersTestControl').catch(() => {
        return { default: () => <div className='error'>Component is not available!</div> };
    })
);
```