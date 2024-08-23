set(Launcher_SVGFileName "${Launcher_AppID}.svg")
set(Launcher_SVGFileName "${Launcher_SVGFileName}" PARENT_SCOPE)

set(Launcher_SVG "assets/${Launcher_SVGFileName}" PARENT_SCOPE)
set(Launcher_Branding_ICNS "assets/prismlauncher.icns" PARENT_SCOPE)
set(Launcher_Branding_ICO "assets/prismlauncher.ico")
set(Launcher_Branding_ICO "${Launcher_Branding_ICO}" PARENT_SCOPE)

configure_file(prismlauncher.ico prismlauncher.ico COPYONLY)
configure_file(${Launcher_SVGFileName} ${Launcher_SVGFileName} COPYONLY)
