if(UNIX)
    find_package(PkgConfig)
    if(PkgConfig_FOUND)
        pkg_search_module(SCDOC scdoc)
        if(SCDOC_FOUND)
            pkg_get_variable(SCDOC_SCDOC scdoc scdoc)
        endif()
    endif()
endif()

set(Launcher_CommonName "PrismLauncher")
set(Launcher_DisplayName "Prism Launcher")

set(Launcher_Name "${Launcher_CommonName}" PARENT_SCOPE)
set(Launcher_DisplayName "${Launcher_DisplayName}" PARENT_SCOPE)

set(Launcher_AppID "org.prismlauncher.PrismLauncher")
set(Launcher_Copyright "© 2022-2025 Prism Launcher Contributors\\n© 2021-2022 PolyMC Contributors\\n© 2012-2021 MultiMC Contributors")
set(Launcher_Copyright_Mac "© 2022-2025 Prism Launcher Contributors, © 2021-2022 PolyMC Contributors and © 2012-2021 MultiMC Contributors" PARENT_SCOPE)
set(Launcher_Copyright "${Launcher_Copyright}" PARENT_SCOPE)
set(Launcher_Domain "prismlauncher.org" PARENT_SCOPE)
set(Launcher_UserAgent "${Launcher_CommonName}/${Launcher_VERSION_NAME}" PARENT_SCOPE)
set(Launcher_ConfigFile "prismlauncher.cfg" PARENT_SCOPE)
set(Launcher_Git "https://github.com/PrismLauncher/PrismLauncher" PARENT_SCOPE)
set(Launcher_AppID "${Launcher_AppID}" PARENT_SCOPE)

set(Launcher_Desktop "packaging/${Launcher_AppID}.desktop" PARENT_SCOPE)
set(Launcher_mrpack_MIMEInfo "packaging/modrinth-mrpack-mime.xml" PARENT_SCOPE)
set(Launcher_MetaInfo "packaging/${Launcher_AppID}.metainfo.xml" PARENT_SCOPE)
set(Launcher_Branding_WindowsRC "packaging/prismlauncher.rc" PARENT_SCOPE)
set(Launcher_Branding_LogoQRC "packaging/prismlauncher.qrc" PARENT_SCOPE)

set(Launcher_Portable_File "packaging/portable.txt" PARENT_SCOPE)

configure_file(${Launcher_AppID}.desktop.in ${Launcher_AppID}.desktop)
configure_file(${Launcher_AppID}.metainfo.xml.in ${Launcher_AppID}.metainfo.xml)
configure_file(prismlauncher.rc.in prismlauncher.rc @ONLY)
configure_file(prismlauncher.qrc.in prismlauncher.qrc @ONLY)
configure_file(prismlauncher.manifest.in prismlauncher.manifest @ONLY)

configure_file(config.wxi.in config.wxi @ONLY)
configure_file(product.wxs product.wxs @ONLY)

if(SCDOC_FOUND)
    set(in_scd "${CMAKE_CURRENT_SOURCE_DIR}/prismlauncher.6.scd")
    set(out_man "${CMAKE_CURRENT_BINARY_DIR}/prismlauncher.6")
    add_custom_command(
        DEPENDS "${in_scd}"
        OUTPUT "${out_man}"
        COMMAND ${SCDOC_SCDOC} < "${in_scd}" > "${out_man}"
    )
    add_custom_target(man ALL DEPENDS ${out_man})
    set(Launcher_ManPage "packaging/prismlauncher.6" PARENT_SCOPE)
endif()
